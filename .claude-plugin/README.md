# ClaudeTailor Plugin

### Plugin Installation

This is a Claude Code plugin that provides AI-driven context provisioning.

#### Quick Install

```bash
# Install from GitHub
claude plugin install https://github.com/John-bardera/ClaudeTailor

# Or add as a marketplace
claude plugin marketplace add https://github.com/John-bardera/ClaudeTailor
```

#### What It Does

ClaudeTailor solves **context bloat** in Claude Code by:
- Dynamically selecting only the relevant rules, MCPs, and skills for your project
- Building minimal `.claude` environments tailored to your development requirements
- Eliminating manual context management

#### Usage

After installation, use the `/tailor` command in any Claude Code session:

```
/tailor Pythonを使用して、株価の時系列データを分析するスクリプトを作成したい。最適な環境を構築して。
```

#### Files Location

When installed, plugin files are located at:
```
~/.claude/plugins/cache/claudetailor/
```

#### Documentation

Full documentation: https://github.com/John-bardera/ClaudeTailor
