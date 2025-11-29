# JSON Canvas 1.0 仕様リファレンス

公式仕様: https://github.com/obsidianmd/jsoncanvas

## ファイル形式

- 拡張子: `.canvas`
- エンコーディング: UTF-8
- 形式: JSON

## トップレベル構造

```json
{
  "nodes": [],
  "edges": []
}
```

両フィールドはオプションだが、通常は少なくとも`nodes`を含む。

---

## ノード（Nodes）

### 共通属性（すべてのノードタイプ）

| 属性 | 型 | 必須 | 説明 |
|------|-----|------|------|
| `id` | string | Yes | キャンバス内で一意の識別子 |
| `type` | string | Yes | `text`, `file`, `link`, `group` のいずれか |
| `x` | integer | Yes | X座標（ピクセル） |
| `y` | integer | Yes | Y座標（ピクセル） |
| `width` | integer | Yes | 幅（ピクセル） |
| `height` | integer | Yes | 高さ（ピクセル） |
| `color` | canvasColor | No | ノードの色 |

### テキストノード（type: "text"）

Markdown形式のテキストを含むノード。

| 属性 | 型 | 必須 | 説明 |
|------|-----|------|------|
| `text` | string | Yes | Markdown構文を含むテキスト |

```json
{
  "id": "abc123",
  "type": "text",
  "x": 0,
  "y": 0,
  "width": 250,
  "height": 100,
  "text": "# タイトル\n\nこれはテキストノードです。"
}
```

### ファイルノード（type: "file"）

ローカルファイルへの参照。

| 属性 | 型 | 必須 | 説明 |
|------|-----|------|------|
| `file` | string | Yes | ファイルパス |
| `subpath` | string | No | 見出し/ブロックへの参照（`#`で始まる） |

```json
{
  "id": "def456",
  "type": "file",
  "x": 300,
  "y": 0,
  "width": 400,
  "height": 300,
  "file": "notes/example.md",
  "subpath": "#section-1"
}
```

### リンクノード（type: "link"）

外部URLへの参照。

| 属性 | 型 | 必須 | 説明 |
|------|-----|------|------|
| `url` | string | Yes | 参照するURL |

```json
{
  "id": "ghi789",
  "type": "link",
  "x": 0,
  "y": 200,
  "width": 300,
  "height": 150,
  "url": "https://example.com"
}
```

### グループノード（type: "group"）

他のノードをグループ化するコンテナ。

| 属性 | 型 | 必須 | 説明 |
|------|-----|------|------|
| `label` | string | No | グループのラベル |
| `background` | string | No | 背景画像のパス |
| `backgroundStyle` | string | No | `cover`, `ratio`, `repeat` のいずれか |

```json
{
  "id": "jkl012",
  "type": "group",
  "x": -50,
  "y": -50,
  "width": 600,
  "height": 400,
  "label": "メイングループ",
  "color": "4"
}
```

---

## エッジ（Edges）

ノード間の接続線。

| 属性 | 型 | 必須 | 説明 |
|------|-----|------|------|
| `id` | string | Yes | 一意の識別子 |
| `fromNode` | string | Yes | 開始ノードのID |
| `fromSide` | side | No | 接続元の辺 |
| `fromEnd` | end | No | 接続元の端点スタイル（デフォルト: `none`） |
| `toNode` | string | Yes | 終了ノードのID |
| `toSide` | side | No | 接続先の辺 |
| `toEnd` | end | No | 接続先の端点スタイル（デフォルト: `arrow`） |
| `color` | canvasColor | No | 線の色 |
| `label` | string | No | エッジのラベル |

### side 型

```
"top" | "right" | "bottom" | "left"
```

### end 型

```
"none" | "arrow"
```

### エッジの例

```json
{
  "id": "edge1",
  "fromNode": "abc123",
  "fromSide": "right",
  "fromEnd": "none",
  "toNode": "def456",
  "toSide": "left",
  "toEnd": "arrow",
  "color": "5",
  "label": "参照"
}
```

---

## canvasColor 型

### プリセットカラー

| 値 | 色 |
|----|----|
| `"1"` | 赤 |
| `"2"` | オレンジ |
| `"3"` | 黄 |
| `"4"` | 緑 |
| `"5"` | シアン |
| `"6"` | 紫 |

### HEXカラー

`#RRGGBB` 形式で任意の色を指定可能。

```json
"color": "#FF5733"
```

---

## 完全なキャンバス例

```json
{
  "nodes": [
    {
      "id": "node1",
      "type": "text",
      "x": 0,
      "y": 0,
      "width": 250,
      "height": 80,
      "text": "# スタート",
      "color": "4"
    },
    {
      "id": "node2",
      "type": "text",
      "x": 350,
      "y": -50,
      "width": 250,
      "height": 80,
      "text": "## オプションA"
    },
    {
      "id": "node3",
      "type": "text",
      "x": 350,
      "y": 50,
      "width": 250,
      "height": 80,
      "text": "## オプションB"
    }
  ],
  "edges": [
    {
      "id": "edge1",
      "fromNode": "node1",
      "fromSide": "right",
      "toNode": "node2",
      "toSide": "left"
    },
    {
      "id": "edge2",
      "fromNode": "node1",
      "fromSide": "right",
      "toNode": "node3",
      "toSide": "left"
    }
  ]
}
```
