---
title: "Site Structure"
description: "my description"
layout: "./docs/template/template.pug"
---

# 3 - サイト構築

## 3.1 - ページの構造

```html
<html>
  <head>
    [metaタグ]
    [tdkタグ + ogタグ]
    [css]
    [headで読み込むJavascript]
  </head>
  <body>
    [bodyの先頭で読み込むJavascript]
    [ヘッダー]
    [コンテンツ]
    [フッター]
    [bodyの末尾で読み込むJavascript]
  </body>
</html>
```
　
現在の HTML 制作用の ejs のスケルトンは上記のような構造になっています。バックエンドへの組み込みや、SPAフレームワークへの組み込みにおいて必要があれば、変わっても問題ありません。

#### Javascript ファイルの読み込み箇所

サイトの動作に必要な Javacript ははすべて domready 時に発動するように実装するため、すべて`<head>`で読み込む仕様で問題ありません。

古いデバイスで、Javascript のファイルロードや評価や実行に時間がかかる場合は、`<body>`の末尾に読み込む事で、Javascript の実行の前に body が描画されるため、ユーザの体感速度を向上させるという手段をチューニングの段階で検討が可能です。  