# Windsurf / Antigravity Rules "v5"

🇬🇧 **English** | 🇯🇵 **日本語**

---

## 🌏 About This Repository / このリポジトリについて

This repository provides custom instructions optimized for **Windsurf** and **Antigravity**.  
It is a port of [cursorrules](https://github.com/kinopeee/cursorrules) adapted for Windsurf Cascade and Antigravity.

このリポジトリは、**Windsurf** および **Antigravity** 用に最適化されたカスタムインストラクションを提供します。  
別リポジトリで公開している [cursorrules](https://github.com/kinopeee/cursorrules) を Windsurf Cascade および Antigravity に移植したものです。

### 📂 Related Repositories / 関連リポジトリ

| Editor | Repository |
|--------|------------|
| **Cursor** | [kinopeee/cursorrules](https://github.com/kinopeee/cursorrules) |
| **Windsurf / Antigravity** | This repository / このリポジトリ |

### 📂 Language-specific Documentation

- 🇯🇵 **日本語版**: [ja/README.md](ja/README.md)
- 🇬🇧 **English**: [en/README.md](en/README.md)

---

## ⚡ Quick Start

### For Windsurf Users

```bash
# Clone the repository / リポジトリをクローン
git clone https://github.com/kinopeee/windsurf-antigravity-rules.git

# Copy to your project / プロジェクトにコピー
cp -r windsurf-antigravity-rules/ja/.windsurf ~/your-project/   # 日本語
cp -r windsurf-antigravity-rules/en/.windsurf ~/your-project/   # English
```

### For Antigravity Users

```bash
# Clone the repository / リポジトリをクローン
git clone https://github.com/kinopeee/windsurf-antigravity-rules.git

# Copy to your project / プロジェクトにコピー
cp -r windsurf-antigravity-rules/ja/.agent ~/your-project/   # 日本語
cp -r windsurf-antigravity-rules/en/.agent ~/your-project/   # English
```

See [ja/README.md](ja/README.md) or [en/README.md](en/README.md) for details.

---

## 📋 What's Included / 含まれるもの

All rule files and workflow commands are available in both Japanese and English.  
すべてのルールファイルとワークフローコマンドに日本語版と英語版があります。

### ✅ Rule Files / ルールファイル

| File | Description |
|------|-------------|
| **v5.md** | Core coding support rules / コーディング支援ルール |
| **commit-message-format.md** | Commit message conventions / コミットメッセージ規約 |
| **pr-message-format.md** | PR message conventions / PRメッセージ規約 |
| **test-strategy.md** | Test strategy rules / テスト戦略ルール |
| **prompt-injection-guard.md** | Injection defense / インジェクション防御 |

### ⚙️ Workflow Commands / ワークフロー

| File | Description |
|------|-------------|
| **commit-only.md** | Commit only / コミットのみ |
| **commit-push.md** | Commit & push / コミット＆プッシュ |
| **commit-push-pr.md** | Commit, push & PR / コミット＆プッシュ＆PR |

> **📍 File Locations / ファイル配置**
>
> | Editor | Rules | Workflows |
> |--------|-------|-----------|
> | **Windsurf** | `.windsurf/rules/` | `.windsurf/workflows/` |
> | **Antigravity** | `.agent/rules/` | `.agent/workflows/` |
>
> For details, see [ja/README.md](ja/README.md) or [en/README.md](en/README.md).

---

## 🎯 Key Features / 主な特徴

### 🇯🇵 日本語

- **GPT-5.1 & Opus 4.5 最適化**: 適応的推論を活かした効率的なタスク実行
- **3段階タスク分類**: 軽量・標準・重要タスクに応じた最適なプロセス
- **並列実行**: 独立したタスクを並列処理して処理速度を向上
- **安全なツール利用**: ファイル読み取り・編集・コマンド実行の明確なポリシー
- **包括的なガードレール**: コミット規約、PR規約、テスト戦略、セキュリティ防御

### 🇬🇧 English

- **GPT-5.1 & Opus 4.5 Optimized**: Efficient task execution leveraging adaptive reasoning
- **3-Tier Task Classification**: Optimal processes for lightweight/standard/critical tasks
- **Parallel Execution**: Improved throughput by parallelizing independent tasks
- **Safe Tool Usage**: Clear policies for file reading, editing, and command execution
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
AI関連情報を X (Twitter) で発信しています: [@kinopee_ai](https://x.com/kinopee_ai)

### 🇬🇧 English

There is no official support for this repository, but feedback is welcome.  
Follow on X (Twitter) for AI-related updates: [@kinopee_ai](https://x.com/kinopee_ai)

---

## Made with ❤️ for Windsurf & Antigravity users worldwide
