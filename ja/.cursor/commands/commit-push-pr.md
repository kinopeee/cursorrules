# コミット・プッシュ・PR作成（一括実行）

## 概要

現在のブランチに対して変更をコミットし、リモートへプッシュしたあと、Pull Request を作成するための一括実行コマンドの例です。  
main/master への直接プッシュ禁止や、コミット前に実行する品質チェック（lint / test / build など）、PR 作成フロー（AI/MCP を使うか、CLI を使うかなど）は、各プロジェクトのポリシーに応じてこのテンプレートを調整してください。

## 前提条件

- 変更済みファイルが存在すること
- リモート `origin` が設定済みであること
- GitHub CLI (`gh`) がインストール済みであること（フォールバック用）
- 作業ブランチ（feature/_, fix/_ など）にいること

## 実行手順（対話なし）

1. ブランチ確認（main/master 直プッシュ防止）
2. 必要に応じて品質チェック（lint / test / build など）を実行
3. 変更のステージング（`git add -A`）
4. コミット（引数または環境変数のメッセージ使用）
5. プッシュ（`git push -u origin <current-branch>`）
6. PR作成（MCP や CLI など、環境に応じた方法で作成）

## 使い方

### A) 最小限の情報で実行（推奨）

コミットメッセージだけ指定し、PR タイトルと本文は AI（MCP 経由など）に任せるパターンです。

```bash
# コミットメッセージのみ指定（例）
MSG="fix: 不要なデバッグログ出力を削除"

# 一括実行
BRANCH=$(git branch --show-current) && \
if [ "$BRANCH" = "main" ] || [ "$BRANCH" = "master" ]; then \
  echo "⚠️ main/master への直接プッシュは禁止です"; exit 1; \
fi

# 任意の品質チェック（必要な場合のみ）
# 例:
# ./scripts/lint.sh && ./scripts/test.sh && ./scripts/build.sh || exit 1

git add -A && \
git commit -m "$MSG" && \
git push -u origin "$BRANCH"

# ここでAIがPR作成を実行（例）
# - ブランチ名から目的を推測
# - git diff --name-status で変更ファイルを確認
# - PRタイトルとメッセージを自動生成
# - mcp_github_create_pull_request / gh pr create 等で PR 作成
```

> 注意: MCP（Model Context Protocol）はエージェントからGitHub等の外部サービスを安全に操作するための標準プロトコルです。本手順ではPR作成にMCPのGitHub連携を使用します。利用にはMCP対応環境の設定が必要です。参考: <https://modelcontextprotocol.io/>

### B) 手動で PR タイトル・メッセージを指定

```bash
# 変数設定
MSG="fix: 不要なデバッグログ出力を削除"
PR_TITLE="fix: 不要なデバッグログ出力を削除"
PR_BODY=$(cat <<'EOF'
## 概要
このPRでは、不要なデバッグログを削除し、ログ出力量を抑制します。

## 変更内容
- 冗長なデバッグログ出力を削除
- 必要なログレベルとメッセージのみを残す

## 技術的な詳細
- 影響範囲はログ出力のみであり、ビジネスロジックには変更なし

## テスト内容
- ログ出力の有無と動作を手動確認

## 関連Issue
Refs #123
EOF
)
# 注意: <<'EOF' (引用符あり) はヒアドキュメント内の変数展開を無効にします。
# PR本文に変数を含めたい場合は、<<EOF (引用符なし) を使用してください。

# 一括実行
BRANCH=$(git branch --show-current) && \
if [ "$BRANCH" = "main" ] || [ "$BRANCH" = "master" ]; then \
  echo "⚠️ main/master への直接プッシュは禁止です"; exit 1; \
fi

# 任意の品質チェック（必要な場合のみ）
# ./scripts/quality-check.sh || exit 1

git add -A && \
git commit -m "$MSG" && \
git push -u origin "$BRANCH" && \
gh pr create --title "$PR_TITLE" --body "$PR_BODY" --base main
```

### C) ステップ実行（デバッグ用）

```bash
# 1) ブランチ確認
BRANCH=$(git branch --show-current)
echo "現在のブランチ: $BRANCH"
if [ "$BRANCH" = "main" ] || [ "$BRANCH" = "master" ]; then
  echo "⚠️ main/master への直接プッシュは禁止です"; exit 1;
fi

# 2) 変更ファイルの確認
echo "変更されたファイル:"
git status --short

# 3) 任意のローカル品質チェック（必要に応じて追加）
# 例:
# echo "品質チェック実行中..."
# ./scripts/lint.sh && ./scripts/test.sh && ./scripts/build.sh || exit 1

# 4) 変更をステージング
git add -A
echo "ステージング完了"

# 5) コミット
MSG="fix: 不要なデバッグログ出力を削除"
git commit -m "$MSG"
echo "コミット完了"

# 6) プッシュ
git push -u origin "$BRANCH"
echo "プッシュ完了"

# 7) PR作成（AIやCLIに依頼）
# この後、AI や gh コマンドなどを使って PR を作成：
# - ブランチ名: $BRANCH
# - 差分: git diff main...HEAD --name-status
# - コミット履歴: git log main..HEAD --oneline
```

## PR自動生成の情報源

AIがPRを作成する際に使用する情報：

```bash
# ブランチ名を取得（目的の推測に使用）
git branch --show-current

# ベースとの差分を取得
git merge-base origin/main HEAD

# 変更ファイルのリスト
git diff --name-status $(git merge-base origin/main HEAD)...HEAD

# 変更の統計情報（必要に応じて）
git diff --stat $(git merge-base origin/main HEAD)...HEAD

# コミット履歴
git log origin/main..HEAD --oneline
```

> **ブランチ参照に関する注意:** 上記のコマンドでは `origin/main`（リモートブランチ）を使用して、最新のリモート状態と比較しています。`gh pr create --base main` で PR を作成する際の `main` 引数は、リモートリポジトリ上のターゲットブランチ名を指します。どちらのアプローチもそれぞれの文脈で正しい使い方です。

## PRタイトルとメッセージのルール

- PR タイトルや本文の詳細なフォーマットは、`.cursor/rules/pr-message-format.mdc` のルールに従ってください。
- 本コマンドは、そのルールで定義された構造化フォーマット（概要／変更内容／テスト内容など）で PR メッセージを記述することを前提としています。

## 注意事項

- コミットメッセージのフォーマットやメッセージ生成の原則は、`.cursor/rules/commit-message-format.mdc` の規約に従ってください。
- `git status` や `git diff` で差分を確認してからの実行を推奨します。

## トラブルシューティング

### プッシュは成功したが PR 作成に失敗した場合

```bash
# PRのみを手動作成
gh pr create --title "タイトル" --body "メッセージ" --base main

# または Web ブラウザで作成
# GitHub 上の対象リポジトリの Pull Requests ページを開き、UI から PR を作成してください。
```

### ブランチ名から Prefix を推測

| ブランチ接頭辞 | Prefix   |
| -------------- | -------- |
| feature/       | feat     |
| fix/           | fix      |
| refactor/      | refactor |
| perf/          | perf     |
| test/          | test     |
| docs/          | docs     |
| build/         | build    |
| ci/            | ci       |
| chore/         | chore    |

## 実行例

```bash
# 例1: 最小限の指定（AIが自動生成）
MSG="fix: 不要なデバッグログ出力を削除"
BRANCH=$(git branch --show-current)
if [ "$BRANCH" = "main" ] || [ "$BRANCH" = "master" ]; then
  echo "⚠️ main/master への直接プッシュは禁止です"; exit 1;
fi

# 任意の品質チェック（必要な場合のみ）
# ./scripts/quality-check.sh || exit 1

git add -A && git commit -m "$MSG" && git push -u origin "$BRANCH"

# この後、AI に以下を依頼：
# "ブランチ $BRANCH に対して PR を作成してください。
#  ブランチ名と差分から適切なタイトルとメッセージを生成してください。"
```

## 関連ドキュメント

- コミットメッセージルール: `.cursor/rules/commit-message-format.mdc`
- PR メッセージルール（任意）: `.cursor/rules/pr-message-format.mdc`
- 開発フロー: プロジェクト固有の README / CONTRIBUTING / 開発ガイド等
