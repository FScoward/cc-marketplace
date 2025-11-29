---
name: polish
description: コード品質チェックを実行するスキル。コード整形（format）、リント（lint）、単体テスト（test）を自動実行する。「コードを整形して」「リントを実行して」「テストを実行して」「コード品質チェック」「polish」などのリクエストで自動発動。
allowed-tools:
  - Bash
  - Read
  - Glob
  - Grep
---

# Polish - コード品質チェックスキル

コード整形、リント、単体テストを実行してコード品質を担保するスキル。

## 実行内容

以下の順序でコード品質チェックを実行する：

1. **コード整形（Format）** - コードスタイルを統一
2. **リント（Lint）** - 静的解析でコード品質をチェック
3. **単体テスト（Test）** - テストを実行して動作を検証

## プロジェクト検出と実行コマンド

プロジェクトルートにある設定ファイルから技術スタックを判定し、適切なコマンドを実行する。

### Kotlin/Gradle プロジェクト

`build.gradle.kts` または `build.gradle` が存在する場合：

```bash
# コード整形
./gradlew ktlintFormat

# リント
./gradlew ktlintCheck

# 単体テスト
./gradlew test
```

### Node.js/npm プロジェクト

`package.json` が存在する場合：

```bash
# コード整形（package.jsonのscriptsを確認）
npm run format  # または npm run prettier

# リント
npm run lint

# 型チェック（TypeScriptの場合）
npm run typecheck  # または npm run type-check

# 単体テスト
npm test  # または npm run test
```

### Python プロジェクト

`pyproject.toml`、`setup.py`、または `requirements.txt` が存在する場合：

```bash
# コード整形
black .  # または ruff format .

# リント
ruff check .  # または flake8 .

# 単体テスト
pytest  # または python -m pytest
```

### Rust プロジェクト

`Cargo.toml` が存在する場合：

```bash
# コード整形
cargo fmt

# リント
cargo clippy

# 単体テスト
cargo test
```

### Go プロジェクト

`go.mod` が存在する場合：

```bash
# コード整形
go fmt ./...

# リント
golangci-lint run

# 単体テスト
go test ./...
```

## 実行手順

1. プロジェクトルートを特定する（git root または カレントディレクトリ）
2. 設定ファイルを確認して技術スタックを判定
3. 各チェックを順番に実行
4. エラーがあれば報告し、修正提案を行う

## 部分実行

ユーザーが特定の処理のみを要求した場合は、その処理のみを実行する：

- 「整形して」「formatして」 → コード整形のみ
- 「リントして」「lintして」 → リントのみ
- 「テストして」「testして」 → 単体テストのみ
- 「全部チェックして」「polishして」 → 全て実行

## 注意事項

- 実行前に `package.json` の scripts セクションを確認し、利用可能なコマンドを把握する
- エラーが発生した場合は、エラー内容を分析して修正案を提示する
- テスト失敗時は失敗したテストケースの詳細を報告する
