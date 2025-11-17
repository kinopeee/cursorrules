# コミット＆プッシュ（現在のブランチ）

## 概要

現在のブランチに対して変更をコミットし、リモートへプッシュします。main/master への直接プッシュは禁止ポリシーのため、ブランチチェックを含みます。`package.json` が存在する場合のみ、コミット前にローカル品質チェック（lint、type-check、build）を実行します。

## 前提条件

- 変更済みファイルが存在すること
- リモート `origin` が設定済みであること
- `package.json` が存在する場合のみ、Node 環境で `npm` コマンドが利用可能であること

## 実行手順（対話なし）

1. ブランチ確認（main/master 直プッシュ防止）
2. `package.json` の存在確認
3. 存在する場合のみ品質チェック（lint:fix → type-check → build）
4. 変更のステージング（`git add -A`）
5. コミット（引数または環境変数のメッセージ使用）
6. プッシュ（`git push -u origin <current-branch>`）

## 使い方

### A) 安全な一括実行（メッセージ引数版）

```bash
MSG="<プレフィックス>: <日本語サマリ>" \
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
```

例：

```bash
MSG="fix: 余計なログ出力を削除" BRANCH=$(git branch --show-current) && \
if [ "$BRANCH" = "main" ] || [ "$BRANCH" = "master" ]; then echo "⚠️ main/master 直プッシュは禁止"; exit 1; fi && \
if [ -f package.json ]; then npm run lint:fix && npm run type-check && npm run build; else echo "ℹ️ package.json が見つかりません。品質チェックをスキップします。"; fi && \
git add -A && git commit -m "$MSG" && git push -u origin "$BRANCH"
```

### B) ステップ実行（読みやすさ重視）

```bash
# 1) ブランチ確認
BRANCH=$(git branch --show-current)
if [ "$BRANCH" = "main" ] || [ "$BRANCH" = "master" ]; then
  echo "⚠️ main/master への直接プッシュは禁止です"; exit 1;
fi

# 2) ローカル品質チェック（package.json が存在する場合のみ）
if [ -f package.json ]; then
  echo "品質チェック実行中..."
  npm run lint:fix && npm run type-check && npm run build || exit 1
else
  echo "ℹ️ package.json が見つかりません。品質チェックをスキップします。"
fi

# 3) 変更をステージング
git add -A

# 4) コミット（メッセージを編集）
git commit -m "<Prefix>: <日本語サマリ>"

# 5) プッシュ
git push -u origin "$BRANCH"
```

## ノート

- コミットメッセージは規約に従ってください（例：`feat: ...`, `fix: ...`）。
- `package.json` が存在しない場合、品質チェックは自動的にスキップされます。
- `package.json` が存在する場合、品質チェックで失敗した場合は、その時点で停止します。修正後に再実行してください。
- 先に `git status` で差分を確認してからの実行を推奨します。
