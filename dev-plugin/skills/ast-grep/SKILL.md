---
name: ast-grep
description: AST（抽象構文木）ベースの構造的コード検索・リファクタリングスキル。「ast-grep」「構造検索」「パターン検索」「コードパターンを探して」「一括置換」などのリクエストで自動発動。
allowed-tools:
  - Bash
  - Read
  - Glob
  - Grep
---

# ast-grep - 構造的コード検索・リファクタリングスキル

ast-grepを使ってAST（抽象構文木）ベースでコードを検索・リファクタリングするスキル。

## ast-grepとは

- テキストベースのgrepとは異なり、コードの構造（AST）を理解して検索
- `$VAR` のようなメタ変数で任意の式やパターンをキャプチャ可能
- 検索結果を構造的に置換してリファクタリング

## 基本コマンド

### 検索（run）

```bash
# パターンで検索
ast-grep run --pattern '$PATTERN' --lang <言語>

# 例: console.log の使用箇所を検索
ast-grep run --pattern 'console.log($MSG)' --lang typescript

# 例: if文の条件部分を検索
ast-grep run --pattern 'if ($COND) { $$$BODY }' --lang kotlin
```

### 置換（rewrite）

```bash
# 対話的に置換
ast-grep run --pattern '$OLD' --rewrite '$NEW' --interactive --lang <言語>

# 例: オプショナルチェーンに変換
ast-grep run --pattern '$A && $A()' --rewrite '$A?.()' --interactive --lang typescript
```

## メタ変数の使い方

| 変数 | 説明 | 例 |
|------|------|-----|
| `$VAR` | 単一のASTノード | `console.log($MSG)` |
| `$$$VARS` | 複数のASTノード（可変長） | `function($$$ARGS)` |
| `$_` | 無視するノード | `if ($_) { $BODY }` |

## 言語指定（--lang）

| 言語 | 指定値 |
|------|--------|
| TypeScript | `typescript`, `ts` |
| JavaScript | `javascript`, `js` |
| Kotlin | `kotlin`, `kt` |
| Python | `python`, `py` |
| Go | `go` |
| Rust | `rust`, `rs` |

## 実行手順

1. ユーザーのリクエストを分析して検索/置換パターンを決定
2. 対象言語を特定（明示的指定またはプロジェクト判定）
3. ast-grepコマンドを構築して実行
4. 結果を報告、必要に応じて置換を提案

## 使用例

### 例1: 非推奨APIの検索
「`useState`の使用箇所を全部探して」
→ `ast-grep run --pattern 'useState($INIT)' --lang typescript`

### 例2: リファクタリング
「`props.onClick && props.onClick()`を`props.onClick?.()`に置換して」
→ `ast-grep run --pattern '$A && $A()' --rewrite '$A?.()' --interactive --lang typescript`

### 例3: 特定パターンの検出
「空のcatchブロックを探して」
→ `ast-grep run --pattern 'catch ($E) {}' --lang typescript`

## 注意事項

- ast-grepがインストールされていない場合は `npm install -g @ast-grep/cli` でインストール
- `--interactive` フラグで変更前に確認可能
- 複雑なパターンはYAMLルールファイルの作成を推奨
