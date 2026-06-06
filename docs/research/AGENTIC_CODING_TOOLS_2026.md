# 2026年時点における自律型コーディングツール比較

> **確認基準日:** 2026年6月
> **位置づけ:** 本文書は、SCAOにおける実装担当AIの代替候補・併用候補を理解するための補足教材である。
> **注意:** 各製品の仕様、料金、提供形態、対応IDEは変更される可能性がある。導入時には公式ドキュメントを再確認すること。

## 1. 結論

Cursor以外にも、コードベースの調査、複数ファイル編集、コマンド実行、テスト、差分確認を支援する自律型コーディングツールが存在する。

ただし、すべての製品がCursorと同一の動作をするわけではない。

製品は、提供形態と主な利用方法を区別して比較する。

## 2. 分類

```text
自律型コーディングツール
├── AI IDE型
│   ├── Cursor
│   └── Devin Desktop（旧 Windsurf）
│
├── IDE拡張・CLI型
│   ├── Cline
│   ├── Claude Code
│   └── OpenAI Codex
│
└── クラウド非同期エージェント型
    ├── GitHub Copilot cloud agent
    ├── Devin
    ├── Cursor Web / cloud agents
    └── Codex Cloud
```

## 3. 比較表

| ツール・サービス名 | 主な提供形態 | 推奨される利用環境 | 開発元 | 主な特徴 | SCAO上の位置づけ | 代表となる公式URL |
| --- | --- | --- | --- | --- | --- | --- |
| Cursor | AI IDE、CLI、Web・クラウドエージェント | Cursor Desktop、ターミナル、Web | Anysphere | AI IDEを中心として、ローカル作業とクラウド作業に対応する | 標準の実装担当 | https://cursor.com/ |
| GitHub Copilot cloud agent | GitHub連携型クラウドエージェント | GitHub、対応IDE | GitHub | リポジトリ調査、計画作成、コード変更、Pull Request作成を支援する | チーム開発時の併用候補 | https://docs.github.com/en/copilot/how-tos/use-copilot-agents/cloud-agent |
| Cline | オープンソースのIDE拡張、CLI | VS Code系エディタ、ターミナル | Clineプロジェクト | ファイル操作、コマンド実行、ブラウザ操作、MCP連携、承認制御に対応する | ローカル中心の代替候補 | https://docs.cline.bot/cline-overview |
| Devin Desktop（旧 Windsurf） | 独立型AI IDE | Devin Desktop | Cognition | 従来のWindsurf IDEを継承し、Agent Command Centerを統合する | AI IDE型の代替候補 | https://docs.devin.ai/desktop/devin-desktop-faq |
| Claude Code | IDE拡張、CLI | ターミナル、対応IDE | Anthropic | コードベース読込、ファイル編集、コマンド実行、開発ツール連携に対応する | ターミナル中心の代替候補 | https://code.claude.com/docs/ja/overview |
| OpenAI Codex | CLI、IDE拡張、Web・クラウド | ターミナル、対応IDE、Codex Cloud | OpenAI | コード読込、変更、実行、クラウド上のバックグラウンド作業に対応する | ローカル・クラウド併用候補 | https://developers.openai.com/codex/cloud |
| Devin | クラウド型AIソフトウェアエンジニア | Web、クラウド環境 | Cognition | コード作成、実行、テスト、バグ修正、Pull Requestレビューなどを支援する | 非同期タスクの委任候補 | https://docs.devin.ai/get-started/devin-intro |

## 4. 実務上の使い分け

### 4.1 Cursor

SCAOの標準実装担当として扱う。

向いている用途:

* 人間が差分を確認しながら進める開発
* SPECに基づく小さな実装単位
* ローカルビルドとテスト
* Git差分確認
* Cursor Rulesによるプロジェクト固有規律の適用

### 4.2 GitHub Copilot cloud agent

GitHub Issue、branch、Pull Requestを中心に運用するチーム開発で有効である。

向いている用途:

* GitHub Issueを起点とする作業依頼
* 非同期の実装修正
* Pull Requestベースのレビュー
* GitHub中心の組織運用

旧GitHub Copilot Workspaceは技術プレビューを終了しているため、2026年時点の現行比較ではGitHub Copilot cloud agentを対象とする。

### 4.3 Cline

使い慣れたVS Code系エディタを維持しながら、自律実行機能を追加したい場合の候補である。

向いている用途:

* ローカルファイルの調査
* ターミナルコマンドの実行
* ビルドとテスト
* ブラウザを利用した確認
* MCPによる機能拡張
* 使用モデルやプロバイダーの選択

注意点:

* 自動承認範囲を広げすぎない。
* API料金や利用上限は、選択したモデルとプロバイダーに依存する。
* 秘密情報、破壊的操作、外部送信の扱いを事前に定義する。

### 4.4 Devin Desktop（旧 Windsurf）

Windsurfの後継名称として提供されるAI IDEである。

向いている用途:

* IDE内のコード変更支援
* ターミナル操作
* MCP連携
* ルールとメモリによるカスタマイズ
* 複数エージェント管理

過去資料との対応関係を明確にするため、当面は「Devin Desktop（旧 Windsurf）」と併記する。

### 4.5 Claude Code

ターミナル中心の開発や、Claudeを実装担当として利用する場合の候補である。

向いている用途:

* コードベース横断調査
* 複数ファイル修正
* コマンド実行
* バグ修正
* IDEとCLIの併用

SCAOでClaudeを監査担当として利用する場合は、監査担当Claudeと実装担当Claude Codeの責務を混同しない。

### 4.6 OpenAI Codex

ローカル作業とクラウド委任を使い分けたい場合の候補である。

向いている用途:

* コード読込、変更、実行
* ターミナル中心の実装
* IDE内の実装支援
* クラウド上のバックグラウンド作業
* 並行タスクの分離

SCAOでChatGPTを設計担当として利用する場合は、設計担当ChatGPTと実装担当Codexの責務を混同しない。

### 4.7 Devin

独立性の高い作業を、クラウド環境へ非同期で委任する場合の候補である。

向いている用途:

* チケット単位の作業
* バグ再現と修正
* 内部ツールの作成
* 並行開発
* Pull Requestレビュー

## 5. 生徒への指導指針

特定ツールの操作方法だけを暗記させない。

次の共通構造を理解させる。

```text
人間がSPECを定義する
  ↓
AIへ対象範囲と変更禁止範囲を示す
  ↓
AIが計画を作成する
  ↓
人間が計画を確認する
  ↓
AIが実装・テストを行う
  ↓
人間が差分・ログ・テスト結果を確認する
  ↓
必要に応じて監査担当AIへレビューを依頼する
```

## 6. 重要な注意事項

自律型AIへ丸投げしてはならない。

最低限、次を人間が確認する。

* SPECとの整合性
* 変更対象ファイル
* 変更禁止範囲への影響
* Git差分
* ビルド結果
* テスト結果
* 秘密情報の混入
* 個人情報の混入
* 破壊的操作の有無
* 外部サービスへの送信範囲
* 復旧方法

## 7. SCAOにおける採用方針

SCAOの標準実装担当は、当面Cursorとする。

他の自律型コーディングツールは、Cursorと完全に同一の製品として扱わない。

プロジェクト、チーム構成、セキュリティ要件、料金体系、利用環境、承認フローに応じて、代替候補または併用候補として評価する。

## 8. 公式情報源

### 8.1 Cursor

* 公式サイト:
  https://cursor.com/

* ダウンロード・提供環境:
  https://cursor.com/download

* 更新履歴:
  https://cursor.com/changelog

### 8.2 GitHub Copilot cloud agent

* 概要:
  https://docs.github.com/en/copilot/concepts/agents/cloud-agent

* 利用方法:
  https://docs.github.com/en/copilot/how-tos/use-copilot-agents/cloud-agent

* セッション開始:
  https://docs.github.com/en/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions

### 8.3 GitHub Copilot Workspace

* 過去の技術プレビュー資料:
  https://githubnext.com/projects/copilot-workspace/

GitHub Copilot Workspaceは、過去の技術プレビューとして扱う。2026年時点の現行比較では、GitHub Copilot cloud agentを対象とする。

### 8.4 Cline

* 公式ドキュメント:
  https://docs.cline.bot/cline-overview

* 利用可能なツール:
  https://docs.cline.bot/tools-reference/all-cline-tools

* Auto Approve・YOLO Mode:
  https://docs.cline.bot/features/auto-approve

* MCP:
  https://docs.cline.bot/mcp/adding-and-configuring-servers

### 8.5 Devin Desktop（旧 Windsurf）

* Devin Desktop FAQ:
  https://docs.devin.ai/desktop/devin-desktop-faq

* 導入ガイド:
  https://docs.devin.ai/desktop/getting-started

### 8.6 Claude Code

* 概要:
  https://code.claude.com/docs/ja/overview

* IDE連携:
  https://code.claude.com/docs/en/ide-integrations

* MCP:
  https://code.claude.com/docs/ja/mcp

### 8.7 OpenAI Codex

* Codex CLI:
  https://developers.openai.com/codex/cli

* Codex Cloud:
  https://developers.openai.com/codex/cloud

* Codex CLI Reference:
  https://developers.openai.com/codex/cli/reference

* 更新履歴:
  https://developers.openai.com/codex/changelog

### 8.8 Devin

* Devin概要:
  https://docs.devin.ai/get-started/devin-intro

* 更新情報:
  https://docs.devin.ai/release-notes/overview

## 9. 更新ルール

本比較表を更新する場合は、次の順序で確認する。

1. 製品名が変更されていないか。
2. 提供形態が変更されていないか。
3. AI IDE型、IDE拡張・CLI型、クラウド非同期型の分類が妥当か。
4. 公式ドキュメントに記載された機能か。
5. 料金、対応OS、対応IDE、利用条件が変更されていないか。
6. SCAOにおける標準採用、代替候補、併用候補の位置づけを変更する必要があるか。

広告的な表現、出典不明のシェア情報、「最強」「最大のライバル」「完全自律」「無限にループする」などの検証困難な断定表現は使用しない。
