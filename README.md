# 👔 ClaudeTailor

> **Stop context bloat. Let AI pick what it needs.**
> Claude Codeのための、AI駆動型コンテキスト・プロビジョニングエンジン

ClaudeTailorは、Claude Codeのプロジェクト環境（`./.claude`）を、その時の開発要件に合わせて**動的かつ最小構成で自動構築**するプラグインです。

---

## 🚨 The Problem: コンテキストの肥大化と管理地獄

Claude Codeを使いこなすにつれ、私たちは優秀な外部MCPやOSSのスキル群を大量に導入したくなります。しかし、それらをすべて読み込ませるとどうなるでしょうか？

* **💸 トークンの浪費:** 使わないツールの説明文でコンテキストウィンドウが埋め尽くされます。
* **🧠 推論の低下（ハルシネーション）:** AIが「今はどのルール・ツールを使うべきか」で迷い、的外れなコードを生成し始めます。
* **📁 管理コストの爆発:** 「Python用」「フロントエンド用」と静的なテンプレートを人間が手動で管理するのは、もはや限界です。

---

## 💡 The Solution: Just-In-Time Context

**ClaudeTailorは、このアプローチを根本から変えます。**
あなたはルールやMCPをフラットな「素材プール」に放り込んでおくだけ。あとはプロジェクト開始時に `/tailor` コマンドを叩けば、**AI自身が要件を解釈し、何百という素材の中から本当に必要なコンテキストだけを抽出（Cherry-pick）**して、専用の環境を仕立て上げます。

* **Bring Your Own Context:** 特定の言語やツールに依存しません。あなた独自の秘伝のプロンプトや、お気に入りのOSSをそのまま活用できます。
* **Zero Taxonomy:** 「このルールはどのフォルダに分類すべきか？」と悩む必要はありません。

---

## 📂 Architecture & Directory Structure

ClaudeTailorは「プラグイン」と「あなたの素材庫（プール）」で構成されます。AIが正確に抽出できるよう、以下のような構造での管理を推奨しています。

```text
ClaudeTailor/
├── README.md
├── .claude-plugin/        # ⚙️ プラグイン定義（plugin.json）
├── skills/                # 🎯 /tailor スキル
├── hooks/                 # 🪝 プロジェクト開始時のフック
├── pool/                  # 📦 【ユーザー定義】あなたのコンテキスト素材庫
│   ├── rules/             #  ├─ 用途がわかる命名のMarkdown (例: python_typing.md, finance_calc.md)
│   ├── mcps/              #  ├─ MCPサーバー設定ファイル (例: sqlite_mcp.json)
│   └── skills/            #  └─ 単一機能のスクリプト群
└── submodules/            # 📦 【ユーザー定義】外部OSSのリンク (Git Submodules等)
```

---

## 🚀 Getting Started

ClaudeTailorを使用するには、リポジトリをクローンしてプラグインとして登録する必要があります。

### ステップ1: リポジトリのClone

まず、リポジトリを作業ディレクトリにクローンします。

```bash
git clone https://github.com/John-bardera/ClaudeTailor.git ~/ClaudeTailor
```

### ステップ2: プラグインの登録

クローンしたディレクトリを、Claude Codeにプラグインとして追加します。

```bash
claude add plugin ~/ClaudeTailor
```

### ステップ3: 素材プールの構築（あなたの色に染める）

`~/ClaudeTailor/pool/` 配下に、普段お使いのRule、MCP、外部スキルを自由に配置してください。

```text
~/ClaudeTailor/pool/
├── rules/     # ルール用Markdownファイル
├── mcps/      # MCPサーバー設定ファイル
└── skills/    # カスタムスキルファイル
```

### ステップ4: プロジェクトの仕立て（環境構築）
新規プロジェクトのディレクトリを作成し、Claude Codeを起動します。

```bash
mkdir my-new-project && cd my-new-project
claude
```

魔法のコマンド `/tailor` を呼び出し、作りたいものの要件を伝えます。

> **User:**
> `/tailor Pythonを使用して、株価の時系列データを分析するスクリプトを作成したい。最適な環境を構築して。`

ClaudeTailorがあなたのプールをスキャンし、現在のプロジェクト（`./.claude`）に「Pythonの型規約」「金融計算用ルール」「データ分析用MCP」など、**必要最小限の設定のみを自動抽出・配置**します。

---

**👔 さあ、無駄のない最高のパフォーマンスを発揮するClaude Code環境を手に入れましょう！**

