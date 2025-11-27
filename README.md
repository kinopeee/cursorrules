# cursorrules "v5"

🇬🇧 **English** | 🇯🇵 **日本語**

---

## 🌏 Select Your Language / 言語を選択

This repository provides custom instructions and custom commands optimized for Cursor.  
このリポジトリは、Cursor 用に最適化されたカスタムインストラクションやカスタムコマンドを提供します。

### 📂 Language-specific Documentation

- 🇯🇵 **日本語版**: [ja/README.md](ja/README.md)
- 🇬🇧 **English**: [en/README.md](en/README.md)

---

## ⚡ Quick Start

### For Japanese Users (日本語ユーザー向け)

```bash
# リポジトリをクローン
git clone https://github.com/kinopeee/cursorrules.git

# 日本語版の設定をプロジェクトにコピー
cp -r cursorrules/ja/.cursor ~/your-project/
```

詳細は [ja/README.md](ja/README.md) をご覧ください。

### For English Users

```bash
# Clone the repository
git clone https://github.com/kinopeee/cursorrules.git

# Copy English configuration to your project
cp -r cursorrules/en/.cursor ~/your-project/
```

See [en/README.md](en/README.md) for details.

---

## 📋 What's Included / 含まれるもの

### ✅ Rule Files (`.cursor/rules/*.mdc`)

| File | 日本語 | English |
|------|--------|---------|
| **v5.mdc** | GPT-5.1最適化のコーディング支援ルール | Coding support rules optimized for GPT-5.1 |
| **commit-message-format.mdc** | コミットメッセージフォーマット規約 | Commit message format conventions |
| **pr-message-format.mdc** | PRメッセージフォーマット規約 | PR message format conventions |
| **test-strategy.mdc** | テスト戦略ルール（等価分割・境界値） | Test strategy rules (equivalence/boundary) |
| **prompt-injection-guard.mdc** | 外部コンテキストインジェクション防御 | External context injection defense |

### ⚙️ Workflow Commands (`.cursor/commands/*.md`)

| Command | 日本語 | English |
|---------|--------|---------|
| **commit-only.md** | コミットのみ実行 | Execute commit only |
| **commit-push.md** | コミット＆プッシュ | Commit and push |
| **commit-push-pr.md** | コミット＆プッシュ＆PR作成 | Commit, push, and create PR |

---

## 🎯 Key Features / 主な特徴

### 🇯🇵 日本語

- **GPT-5.1 & Opus 4.5 最適化**: 適応的推論を活かした効率的なタスク実行
- **3段階タスク分類**: 軽量・標準・重要タスクに応じた最適なプロセス
- **並列実行**: 独立したタスクを並列処理して処理速度を向上
- **安全なツール利用**: read_file/apply_patch/run_terminal_cmd の明確なポリシー
- **包括的なガードレール**: コミット規約、PR規約、テスト戦略、セキュリティ防御

### 🇬🇧 English

- **GPT-5.1 & Opus 4.5 Optimized**: Efficient task execution leveraging adaptive reasoning
- **3-Tier Task Classification**: Optimal processes for lightweight/standard/critical tasks
- **Parallel Execution**: Improved throughput by parallelizing independent tasks
- **Safe Tool Usage**: Clear policies for read_file/apply_patch/run_terminal_cmd
- **Comprehensive Guardrails**: Commit conventions, PR conventions, test strategy, security defense

---

## 📖 Documentation / ドキュメント

### 🇯🇵 日本語

- [使い方ガイド](ja/README.md)
- [変更履歴](ja/CHANGELOG.md)
- [ルールとワークフロー](ja/doc/rules-and-workflows.md)
- [プロンプトインジェクション防御](ja/doc/prompt-injection-guard.md)

### 🇬🇧 English

- [Usage Guide](en/README.md)
- [Changelog](en/CHANGELOG.md)
- [Rules and Workflows](en/doc/rules-and-workflows.md)
- [Prompt Injection Guard](en/doc/prompt-injection-guard.md)

---

## 📄 License / ライセンス

MIT License - See [LICENSE](LICENSE) for details.  
MITライセンス - 詳細は [LICENSE](LICENSE) を参照してください。

---

## 💬 Support / サポート

### 🇯🇵 日本語

このリポジトリに公式サポートはありませんが、フィードバックは歓迎します。  
Cursor関連情報を X (Twitter) で発信しています: [@kinopee_ai](https://x.com/kinopee_ai)

### 🇬🇧 English

There is no official support for this repository, but feedback is welcome.  
Follow on X (Twitter) for Cursor-related updates: [@kinopee_ai](https://x.com/kinopee_ai)

---

## Made with ❤️ for Cursor IDE users worldwide
