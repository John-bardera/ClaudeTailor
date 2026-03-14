# tailor skill

## 説明
プロジェクトの要件に基づいて、最適なClaude Code環境（`.claude/`）を動的に構築します。ユーザーのコンテキストプールから必要なルール、MCP、スキルをAIが自動選択・抽出します。

## 使用方法
/tailor [プロジェクトの要件や目的の説明]

## 実装

### ステップ1: 要件の分析
ユーザーの入力から以下を分析します：
- 使用するプログラミング言語
- プロジェクトの種類（Web開発、データ分析、CLIツールなど）
- 必要な機能や要件
- 関連するドメイン知識

### ステップ2: コンテキストプールの確認
`~/ClaudeTailor/pool/` ディレクトリ以下から、関連するコンテキストを検索します：
- `pool/rules/` - プロジェクトルール（Markdownファイル）
- `pool/mcps/` - MCPサーバー設定（JSONファイル）
- `pool/skills/` - カスタムスキル
- `submodules/` - 外部OSSプロジェクト

### ステップ3: 関連コンテキストの抽出
要件に基づいて、以下の基準でコンテキストを選択します：
1. **直接的関連性**: ファイル名や内容にキーワードが含まれる
2. **間接的関連性**: 説明文から推測される関連性
3. **汎用的価値**: どのプロジェクトでも役立つ基本設定

### ステップ4: 環境の構築
選択したコンテキストを現在のプロジェクトの `.claude/` ディレクトリに配置します：
- ルール → `.claude/rules/`
- MCP設定 → `.claude/mcp.json` にマージ
- スキル → `.claude/skills/`

### ステップ5: サマリーの表示
構築した環境のサマリーを表示します：
```
✅ ClaudeTailor: Environment built for [要件]

Added rules:
  - [ルール名]

Configured MCPs:
  - [MCP名]

Added skills:
  - [スキル名]

Ready to start development! 🎯
```

## 例

### Web開発プロジェクト
```
/tailor ReactとTypeScriptを使ったWebアプリケーションを作成したい
```

→ 抽出: Reactのベストプラクティス、TypeScript型ルール、ESLint設定、フロントエンド開発スキル

### データ分析プロジェクト
```
/tailor Pythonで株価の時系列データを分析するスクリプトを作成したい
```

→ 抽出: Python型規約、データ分析用ルール、Jupyter関連設定、pandas/numPyスキル

## ノート

### Bring Your Own Context
ユーザーは独自のルールやスキルを `pool/` ディレクトリに自由に追加できます。特定の言語やツールに依存しません。

### Zero Taxonomy
コンテキストを分類する必要はありません。AIがファイル名と内容から適切に判断します。
