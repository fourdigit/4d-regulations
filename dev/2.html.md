---
title: "HTML"
description: "my description"
layout: "./docs/template/template.pug"
---

# 2 - マークアップ

## 2.1 - 設計

### 2.1.1 - html5 基準

HTML5 基準でのマークアップを推奨します。

* 廃れたタグ要素は使用しない。  
  （applet，basefont，center，font，s，strike，u，blink，marquee）
* レイアウトに関する属性は使用しない。  
  （align，alink，border，bgcolor，background，clear，code，color，face，height，hspace，language，link，nowrap，text，size，value，vlink，space，width）
* html5 では閉じタグは必須ではありませんが、React 等 jsx シンタックスへの移行がしやすいように、タグは必ず閉じる事を推奨します。
* テーブルやフレームセットでのレイアウトは使用しない。
* 機種依存文字は使用しない。HTML で直接記述できない文字や記号を使う際は文字実態参照を使用する。以下にその例を挙げる。

| 文字実体参照 | 表示                            |
| :----------- | :------------------------------ |
| &quot;       | " 引用符                        |
| &nbsp;       | 改行無し空白（Not Break Space） |
| &apos;       | アポストロピィー                |
| &amp;        | & アンドマーク（ampersand）     |
| &lt;         | < 小なり（less than）           |
| &gt;         | > 大なり（greater than）        |
| &copy;       | © コピーライト                  |
| &reg;        | ® 登録商標（Registered Sign）   |
| &trade;      | TM トレードマーク               |

### 2.1.2 - ejs を用いた静的 HTML のコーディング

静的 HTML のマークアップには、ejsやPugなどテンプレートを用いてモジュールを意識した実装を推奨しています。  

### 2.1.2 - id 及び class の名称

1 つ画面内で同一 id が 2 つ以上存在してはならないため、  
要素の特定は基本的に「id」属性は極力使わず、「class」属性を使います。  
※ body 要素の「id」属性を指定して、固有ページを特定する際に使用する事は問題ありません。

| id 及び class 名称 | 内容                                                                       |
| :----------------- | :------------------------------------------------------------------------- |
| wrapper            | ページ全体                                                                 |
| header             | ヘッダー                                                                   |
| container          | ボディ                                                                     |
| footer             | フッター                                                                   |
| primary            | 2 段組みレイアウトの主要素                                                 |
| secondary          | 2 段組みレイアウトの副要素                                                 |
| gnav               | グローバルナビゲーション                                                   |
| lnav               | ローカルナビゲーション                                                     |
| content            | 主要コンテンツ                                                             |
| sidebar            | サイドバー                                                                 |
| contentbox         | コンテンツを内包するボックス                                               |
| ban                | バナー(※banner や ad の場合は広告駆除ツールで駆除されてしまう可能性がある) |
| pagetop            | ページトップ                                                               |
| category           | カテゴリー                                                                 |

## 2.2 - ベストプラクティス

### 2.2.1 - 文字コードは UTF-8

文字コードは基本的に UTF-8（BOM 無し）を推奨します。  
多言語対応要件や、フィーチャーフォン対応要件などで文字コード指定がある場合は、指定文字コードを採用します。

### 2.2.2 - lang 属性

* 文書の言語コードを指定する。基本的には`"ja"`となるが、html テキストや、公開する国に応じて適切な言語コードを設定する。

### 2.2.3 - IE 互換モード

* 特に理由がない限りは`IE=Edge`を指定し最新版での動作を指定する。
* GCF は開発及び提供終了のため`chrome=1`は記述しない。
* 記述順序によっては動作しないケースがあるため，head 要素の最初に記述する。

### 2.2.4 - viewport 指定

* PC 用のコンテンツであっても、SP でのアクセスも想定し設定する。
* 属性値はコンテンツによって自由に変更可能とする。

### 2.2.5 - format-detection 設定

* SP 等の端末によっては意図せずにリンクが張られることがある為、予め無効化しておく。

### 2.2.6 - TDK

TDK(title,description,keywords) はコーディング開始前にサイトマップ（ファイル名一覧）と同時に作成し、ディレクターはマークアップエンジニアに、スプレッドシートファイルまたはプレーンテキストを展開する。

```html
<!DOCTYPE html>
<html lang="ja"
      xmlns="http://www.w3.org/1999/xhtml"
      xmlns:og="http://ogp.me/ns#"
      xmlns:fb="http://www.facebook.com/2008/fbml"
      xmlns:mixi="http://mixi-platform.com/ns#"
      xmlns:gr="http://gree.jp/ns">
<head>
  <!-- meta -->
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, user-scalable=no" />
  <meta name="apple-mobile-web-app-capable" content="yes">
  <meta name="format-detection" content="telephone=no" />
  <meta name="robots" content="noindex,nofollow" />

  <!-- links -->
  <link rel="manifest" href="./manifest.json">
  <link rel="apple-touch-icon" sizes="57x57" href="./favicon/apple-touch-icon-57x57.png">
  <link rel="apple-touch-icon" sizes="60x60" href="./favicon/apple-touch-icon-60x60.png">
  <link rel="apple-touch-icon" sizes="72x72" href="./favicon/apple-touch-icon-72x72.png">
  <link rel="apple-touch-icon" sizes="76x76" href="./favicon/apple-touch-icon-76x76.png">
  <link rel="apple-touch-icon" sizes="114x114" href="./favicon/apple-touch-icon-114x114.png">
  <link rel="apple-touch-icon" sizes="120x120" href="./favicon/apple-touch-icon-120x120.png">
  <link rel="apple-touch-icon" sizes="144x144" href="./favicon/apple-touch-icon-144x144.png">
  <link rel="apple-touch-icon" sizes="152x152" href="./favicon/apple-touch-icon-152x152.png">
  <link rel="apple-touch-icon" sizes="180x180" href="./favicon/apple-touch-icon-180x180.png">
  <link rel="icon" type="image/png" sizes="192x192" href="./favicon/android-chrome-192x192.png">
  <link rel="icon" type="image/png" sizes="48x48" href="./favicon/favicon-48x48.png">
  <link rel="icon" type="image/png" sizes="96x96" href="./favicon/favicon-96x96.png">
  <link rel="icon" type="image/png" sizes="96x96" href="./favicon/favicon-160x160.png">
  <link rel="icon" type="image/png" sizes="96x96" href="./favicon/favicon-196x196.png">
  <link rel="icon" type="image/png" sizes="16x16" href="./favicon/favicon-16x16.png">
  <link rel="icon" type="image/png" sizes="32x32" href="./favicon/favicon-32x32.png">

  <!-- description -->
  <title>title</title>
  <meta name="description" content="[description]">
  <meta name="keywords" content="[keywords]">
  <link rel="canonical" href="http://domain.com/">
  <meta property="og:title" content="title" />
  <meta property="og:type" content="website" />
  <meta property="og:url" content="http://domain.com/" />
  <meta property="og:image" content="/opg.png" />
  <meta property="og:description" content="[description]" />

  <!-- stylesheets -->
  <link rel="stylesheet" href="/assets/app/css/app.css" />
  <!-- javascripts -->
  <script src="/assets/app/js/app.js"></script>
</head>
```

#### title

タイトル文字列には「商品を表すキーワード」を必ず入れておき，日本語で全角 35 文字以内で記述する。

```
<title>キーワード | 社名・サイト名</title>
```

```
<title>ブランド | カテゴリ | ページ名 | 社名</title>
```

#### description

全角 75 文字以内でウェブページの要約文、説明文を記述する。

#### keywords

キーワードはウェブページに関連するワードをカンマ区切りで 10 つまで記述する。(SEO的に効果がないとされるため、最近では記載しないこともある)

### 2.2.7 - canonical 設定

セッション ID などの訪問者識別用パラメータを使っている場合や、EC サイトにおいてパラメータで指定する等の場合、SEO 的には別ページと解釈されるため、同一のページであることを明示する。

### 2.2.8 - OGP（Open Graph Protocol）

Facebookなどに「シェア」される際に、デフォルトで出力されるタイトルやサムネイルなどの情報を定義する。

### 2.2.9 - favicon

* 多くのモダンブラウザでは「お気に入り」や「タイル」「サムネイル」などで favicon を取得しており、ユーザはそのウェブページに対して、ページを開くことなくブランドを感じることができる。
* 作成するには、16x16 の PNG を作成し、favicon 生成ツール ([http://www.favicon.cc/](http://www.favicon.cc/)など) を使用して ico 形式にし、ウェブページの HTML メタタグで適切に場所を指定する。
* コーポレートロゴでは小さすぎて判別がつきにくい、もしくは潰れてしまう場合は、ビールの会社であればビールのグラフィックなどのピクトグラムも有効である。但しブランドトーンは踏襲すること。

#### 2.2.10 - Apple iOS Icons

* Apple 製の iOS デバイスではウェブページを「お気に入り」の代わりに「ホーム画面に追加」すると、画面全体をキャプチャしてホーム画面のアイコンとして使用される。しかし、ウェブページが縮小されてアイコンになっているために、ユーザは何のサイトか判断することが難しい。
* ページを開かなくてもブランドを感じることができるよう、favicon と同様 iOS icon も指定する。多くのウェブページではブランドロゴを入れるのが主である。
* 57 x 57、72 x 72、114 x 114、144 x 144 の解像度で PNG 画像を作成し、適切なメタタグを指定する。ただし可能な限り圧縮と減色を行い、40KB 以内に収まるようにする。
