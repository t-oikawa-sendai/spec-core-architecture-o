# Repository Implementation Rules (SKILL)

本リポジトリにおけるCursorの実装、および手書きコードは、以下の規律を強制遵守しなければならない。本ファイルはコード署名および構文ルールの「唯一の正本（Single Source of Truth）」である。

## 1. Mandatory Code Header Comments

### 適用対象
* Cursorまたは人間が直接管理するJava、Python、HTML等のソースコード
* 新規作成または内容変更を行う対象ファイル

### 除外対象
* 自動生成ファイル
* 外部依存ファイル
* lockファイル
* バイナリ
* コメント非対応形式
* 先頭行にshebang、XML宣言、その他の必須宣言が必要なファイル

先頭宣言が必要な場合、宣言の直後へヘッダーコメントを記載する。

### Java (JUnitテストコード含む)
```java
/*
 * Program Name:
 * Language: Java
 * Function:
 * Created:
 * Last Updated:
 * Author: Takashi Oikawa
 * AI: Cursor
 * Memo:
 */
```

### Python (pytestコード含む)
```python
# Program Name:
# Language: Python
# Function:
# Created:
# Last Updated:
# Author: Takashi Oikawa
# AI: Cursor
# Memo:
```

### HTML
```html
<!--
 * Program Name:
 * Language: HTML
 * Function:
 * Created:
 * Last Updated:
 * Author: Takashi Oikawa
 * AI: Cursor
 * Memo:
 -->
```

### AI表記
`AI: Cursor` を固定値として強制しない。

* Cursorが変更した場合は `AI: Cursor` とする。
* 人間のみで変更した場合は `AI: N/A` とする。

### コメント非対応形式（JSON等）の救済策
JSONなどコメントを挿入できない厳格なフォーマットの場合、原則としてメタファイルを自動生成しない。必要性がSPECまたは指示書で明示された場合のみ、同一ディレクトリに `<対象ファイル名>.meta.md` を作成し、上記と同一のヘッダーフィールドをMarkdown形式で記録すること。

## 2. No-Omission & Test-Driven Implementation Rule

ユーザーの実装スキルが初学者であることを前提に行動せよ。

### コード省略禁止（実ファイルに対する規律）
* 実ファイル内に未完成コード、仮実装、説明用プレースホルダーを残してはならない。
* `TODO` を残す場合は、Ownerの承認と理由の記載を必須とする。
* 実装後は変更ファイル、差分要約、検証結果を報告する。
* 全ソースコード表示はOwnerが要求した場合のみ行う。チャット欄への全コード貼り付けを強制しない。

### テスト規律
* ロジック変更時は、責務と入力型に応じた正常系、異常系、境界値を検討する。
* 適用可能な場合は、異常系または境界値を最低3ケース含める。
* 文言修正、CSS修正、ドキュメント修正など、単体テストが不要な変更では理由を報告する。
* テスト追加が不要と判断した場合は、その理由を明示する。
