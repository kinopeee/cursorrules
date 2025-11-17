# コミット・プッシュ・PR作成（一括実行）

## 概要

現在のブランチに対して変更をコミットし、リモートへプッシュ後、Pull Requestを作成します。main/masterへの直接プッシュは禁止ポリシーのため、ブランチチェックを含みます。`package.json` が存在する場合のみ、コミット前にローカル品質チェック（lint、type-check、build）を実行します。

## 前提条件

- 変更済みファイルが存在すること
- リモート `origin` が設定済みであること
- `package.json` が存在する場合のみ、Node 環境で `npm` コマンドが利用可能であること
- GitHub CLI (`gh`) がインストール済みであること（フォールバック用）
- 作業ブランチ（feature/_, fix/_ など）にいること

## 実行手順（対話なし）

1. ブランチ確認（main/master 直プッシュ防止）
2. `package.json` の存在確認
3. 存在する場合のみ品質チェック（lint:fix → type-check → build）
4. 変更のステージング（`git add -A`）
5. コミット（引数または環境変数のメッセージ使用）
6. プッシュ（`git push -u origin <current-branch>`）
7. PR作成（MCP優先、失敗時はCLI）

## 使い方

### A) 最小限の情報で実行（推奨）

AIがブランチ名と差分から自動でPRタイトルとメッセージを生成します。

```bash
# コミットメッセージのみ指定
MSG="fix: CSRF検証をテスト環境でスキップ"

# 一括実行
BRANCH=$(git branch --show-current) && \
if [ "$BRANCH" = "main" ] || [ "$BRANCH" = "master" ]; then \
  echo "⚠️ main/master への直接プッシュは禁止です"; exit 1; \
fi && \
if [ -f package.json ]; then \
  npm run lint:fix && npm run type-check && npm run build; \
else \
  echo "ℹ️ package.json が見つかりません。品質チェックをスキップします。"; \
fi && \
git add -A && \
git commit -m "$MSG" && \
git push -u origin "$BRANCH"

# ここでAIがPR作成を実行
# - ブランチ名から目的を推測
# - git diff --name-status で変更ファイルを確認
# - PRタイトルとメッセージを自動生成
# - mcp_github_create_pull_request でPR作成
```

> 注意: MCP（Model Context Protocol）はエージェントからGitHub等の外部サービスを安全に操作するための標準プロトコルです。本手順ではPR作成にMCPのGitHub連携を使用します。利用にはMCP対応環境の設定が必要です。参考: https://modelcontextprotocol.io/

### B) 手動でPRタイトル・メッセージを指定

```bash
# 変数設定
MSG="fix: CSRF検証をテスト環境でスキップ"
PR_TITLE="fix: テスト環境でCSRF検証をスキップする機能を追加"
PR_BODY=$(cat <<'EOF'
## 概要
テスト環境でCSRF検証を自動的にスキップする機能を実装しました。

## 変更内容
- lib/api-client.ts に CSRF スキップロジックを追加
- 環境変数 NODE_ENV が test の場合は検証をスキップ
- 既存の本番環境での動作には影響なし

## 技術的な詳細
- shouldSkipCSRF() 関数を追加
- テスト実行時のパフォーマンス向上

## テスト内容
- ユニットテストで動作確認済み
- 本番環境での影響なしを確認

## 関連Issue
Refs #123
EOF
)

# 一括実行
BRANCH=$(git branch --show-current) && \
if [ "$BRANCH" = "main" ] || [ "$BRANCH" = "master" ]; then \
  echo "⚠️ main/master への直接プッシュは禁止です"; exit 1; \
fi && \
if [ -f package.json ]; then \
  npm run lint:fix && npm run type-check && npm run build; \
else \
  echo "ℹ️ package.json が見つかりません。品質チェックをスキップします。"; \
fi && \
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

# 3) ローカル品質チェック（package.json が存在する場合のみ）
if [ -f package.json ]; then
  echo "品質チェック実行中..."
  npm run lint:fix && npm run type-check && npm run build || exit 1
else
  echo "ℹ️ package.json が見つかりません。品質チェックをスキップします。"
fi

# 4) 変更をステージング
git add -A
echo "ステージング完了"

# 5) コミット
MSG="fix: CSRF検証をテスト環境でスキップ"
git commit -m "$MSG"
echo "コミット完了"

# 6) プッシュ
git push -u origin "$BRANCH"
echo "プッシュ完了"

# 7) PR作成（AIに依頼）
# この後、AIが以下の情報を使ってPRを作成：
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

## PRタイトルとメッセージのルール

### タイトルフォーマット

```
<Prefix>: <日本語要約（命令形/簡潔に）>
```

Prefix例：

- `feat:` - 新機能の追加
- `fix:` - バグ修正
- `refactor:` - リファクタリング
- `perf:` - パフォーマンス改善
- `test:` - テスト追加/修正
- `docs:` - ドキュメント更新
- `build:` - ビルド/依存関係の変更
- `ci:` - CI関連の変更
- `chore:` - 雑務

### メッセージ構造（必須）

```markdown
## 概要

このPRで実装した内容の要約を記載

## 変更内容

- 変更点1の説明
- 変更点2の説明
- 変更点3の説明

## 技術的な詳細

必要に応じて実装の詳細を記載

## テスト内容

- 実施したテストの概要
- 動作確認の結果

## 関連Issue

Closes #123
Refs #456
```

## 注意事項

- コミットメッセージは規約に従ってください（例：`feat: ...`, `fix: ...`）
- `package.json` が存在しない場合、品質チェックは自動的にスキップされます
- `package.json` が存在する場合、品質チェックで失敗した場合は、その時点で停止します。修正後に再実行してください
- `git status` で差分を確認してからの実行を推奨します
- PRタイトルは50文字以内、日本語で簡潔に
- PRメッセージは構造化フォーマット必須（緊急修正以外）
- `\n` などのエスケープシーケンスを直接使用しない

## トラブルシューティング

### プッシュは成功したがPR作成に失敗した場合

```bash
# PRのみを手動作成
gh pr create --title "タイトル" --body "メッセージ" --base main

# またはWebブラウザで作成
# https://github.com/kinopeee/chatnative-v1-design/pulls
```

### ブランチ名からPrefixを推測

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
MSG="fix: CSRF検証をテスト環境でスキップ"
BRANCH=$(git branch --show-current)
if [ "$BRANCH" = "main" ] || [ "$BRANCH" = "master" ]; then
  echo "⚠️ main/master への直接プッシュは禁止です"; exit 1;
fi
if [ -f package.json ]; then
  npm run lint:fix && npm run type-check && npm run build
else
  echo "ℹ️ package.json が見つかりません。品質チェックをスキップします。"
fi && \
git add -A && git commit -m "$MSG" && git push -u origin "$BRANCH"

# この後、AIに以下を依頼：
# "ブランチ fix/http-client-skip-csrf-for-tests に対してPRを作成してください。
#  ブランチ名と差分から適切なタイトルとメッセージを生成してください。"
```

## 関連ドキュメント

- コミットメッセージルール: `.cursor/rules/git-commit-message-format.mdc`
- PRフォーマットルール: `.cursor/rules/pr-format.mdc`
- 開発フロー: `docs/local-development-guide.md`
