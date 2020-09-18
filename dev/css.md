---
title: "CSS"
description: "my description"
layout: "./docs/template/template.pug"
---

# 3 - CSS

## 3.1 - 設計

### 3.1.1 - Atomic Design + BEM 設計思想

CSS は かならずなんらかの一貫したルールにしたがって記述してください。
特に精通しているルールがない場合、Atomic DesignとBEMを組み合わせての制作を推奨しています。  
BEM = Block Element Modifier  
参考）  
[http://getbem.com/](http://getbem.com/)  
[https://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/](https://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)  
[https://www.lullabot.com/articles/bem-atomic-design-a-css-architecture-worth-loving](https://www.lullabot.com/articles/bem-atomic-design-a-css-architecture-worth-loving)  
[http://bradfrost.com/blog/post/atomic-web-design/](http://bradfrost.com/blog/post/atomic-web-design/)  
[ABEM. A more useful adaptation of BEM.](https://css-tricks.com/abem-useful-adaptation-bem/)  


### 3.1.2 - SCSS 利用

CSS の記述には SCSS というメタ言語を使用することを推奨します。  
シンタックスは基本的に CSS と同じですが、主に次のような可読性・メンテ性向上させる機能が使えます：

* **import 機能**：import 機能を使用し、複数のソースを 1 つの CSS にビルドする事が出来ます。import されるだけのファイルはファイル名の先頭に _ をつけます。
* **変数**：値を変数かする事が出来ます。
* **関数**：同等な定義は関数化する事で多重な記述が不要になります。
* **定義のネスト化**：selector をネストして定義出来るため、CSS 特有の冗長な記述が不要になります。

参考）  
[https://sass-lang.com/guide](https://sass-lang.com/guide)

※Stylus, lessについてはシェアが下がっており、周辺ツール含めた環境がいつまで維持できるか不明なため、推奨しません。
※十分な理解がある場合、PostCSSのみを利用するかたちでもOKです。web標準に乗る見込みが低いルールはあまり推奨しません。

### 3.1.3 - ソース SCSS を分ける粒度

SCSS ソースファイルは、Atomic Design 思想に準じて、  
基本的には、atom、molecule、organism 単位で分けます。

格納先は

| フォルダー                   | 説明                                                                                        |
| ---------------------------- | ------------------------------------------------------------------------------------------- |
| /assets/css/app/00-base      | 変数、関数、reset 用 CSS、素要素の基本属性などの設定ファイル設置場所                        |
| /assets/css/app/01-atoms     | atom 類の格納 atom の記述は少ないため、1 つのファイルにまとまっていても問題ありません。 |
| /assets/css/app/02-molecules | molecule 類の格納                                                                           |
| /assets/css/app/03-organisms | organism 類の格納                                                                           |
| /assets/css/app/04-templates | ページパターン毎に template を定義し、テンプレート特有のファイルを格納                      |
| /assets/css/app/05-pages     | ページ特有のファイルを格納 ※ 基本的には極力定義しない                                    |

### 3.1.4 - 命名規則

* Class や id の指定はすべて小文字で指定する事を推奨します。  
  （css はエラーが明確に出ないため、大文字小文字を混在させない事で単純ミスを極力減らせます）
* BEM 設計に沿って、`block__element--modifier`という形式で指定します。
* `block`の部分は Atomic Design 思想のどのレイヤーの要素に該当するかわかりやすくするように、block 名の先頭に atom、molecule、organism、template、page の頭文字を付けます。  
  例）
  * atom → a-someelement
  * molecule → m-someelement
  * organism → o-someelement
  * template → t-sometemplate
  * page → p-somepage

### 3.1.5 - LINT

SASS の記述フォーマットをプロジェクト内で統一するために「stylelint」の使用を推奨します。  https://github.com/fourdigit/gulpset での利用例を参考にしてください。
sass-lintについては、Prettierとの連携がうまくいかないことや、メンテナンスがあまり活発でないことを踏まえ推奨しません。

※ lint から ignore したいファイルや行がある場合は、仕様統制者と事前に確認して行ってください。

### 3.1.6 コーディングガイドライン

AirBnb の CSS スタイルガイドラインを参考してください。  
[https://github.com/airbnb/css](https://github.com/airbnb/css)

## 3.2 - ベストプラクティス

### 3.2.1 - 文字コードは UTF-8

文字コードは基本的に UTF-8(BOMなし) を推奨します。

### 3.2.2 - z-index の定義

要素の深度の定義は基本的に DOM の順番で定義する事を推奨します。（後指定 → 前面）  
DOM 構造的にやむ得ない場合のみ z-index を使いましょう。

しかし、z-index を個別に定義してしまうと、全体的な把握が難しくなってしまうため、
`_z-index.scss`にすべての z-index 定義を集約する事を推奨します。

※ z-index の定義は仕様統制者との認識合わせが必要になります。

### 3.2.3 - url 指定は相対で指定

パス構造の変更に対して柔軟に対応できるようにするため、background などで指定する「url」値は絶対パスではなく、css ファイルからの相対で指定する事を推奨します。

### 3.2.4 - 厳密過ぎる DOM 構造指定を避ける

バックエンド組み込みやSPA組み込みの際に、仕組み上必要な div や span 要素を差し込む必要が発生し DOM 構造が完全再現出来ない場合を考慮して、厳密過ぎる DOM 構造指定を避ける事を推奨します。

* nth-child()などの順番指定 → class(modifier) を定義して回避
* `>` 直下指定 → child 要素として指定できない場合は、class(modifier) を定義して回避  
  ※ どうしても上記のような指定が必要な場合は、バックエンドテンプレート組み込みや、Reactアプリケーション化に影響しない事をケース・バイ・ケースで確認する必要があります。

### 3.2.5 - vendor prefix

対応ブラウザに応じて必要な vendor prefix を指定する必要があります。基本的には、PostCSSなどでAutoprefixerをつけて、手で書かないようにしてください。

### 3.2.6 - !important

`!important` 設定をしてしまうと、属性の設定が強すぎて、該当要素の再利用が難しくなってしまう可能性があります。そのため、属性の強さは、css 定義の厳密性で指定する事を推奨します。  
※ `!important`の定義は仕様統制者との認識合わせが必要になります。

### 3.2.7 - `blur` / 多重の`opacity`

広い範囲での CSS のぼかし（`blur`）効果や半透明要素(`opacity`, `rgba`)を多重に重ねると、描画の負荷が高まり、フロントエンドの性能が低下してしまいます。

`blur` を使用する場合は、性能を監視しつつ、限定的な範囲に適用する事。半透明の要素の重なりは 2〜3 個程度に抑える事。

### 3.2.8 - アニメーションの定義

アニメーションはJavaScript で実施せず、CSS transition を設定し、状態の変化を指定するクラスを定義してアニメーションさせる事を推奨します。(画面ロード時のアニメーションや、複雑な流れのあるアニメーション、要素の幅や高さ計測が必要なアニメーションについてはこの限りではありません)

例）

```css
.o-sample {
  transition: all 0.5s;
  height: 100px;
  background: #f00;

  &.is-open {
    height: 400px;
    background: #0f0;
  }
}
```

### 3.2.9 - CSS ハック

使用してはいけない。コードリーディングの予備知識として以下を記しておく。

- アンダースコアハック（プロパティの先頭にアンダースコア`_`をつけると、IE のみを適用対象）
- スターハック（プロパティの先頭にアスタリスク*をつけると Windows 版 IE のみ適用対象）
- あるいは Windows 版 IE7 のみのハック（「*+html」というセレクタは Windows 版 IE7 のみ適用可能）

### 3.2.10 - フォント指定

- コーディング開始前に、html, bodyレベルで共通のフォントを当てる。
- 混植する場合、英字・日本語の順番で指定する。
- 役物の文字詰めにこだわりたい案件の場合、 https://qrac.github.io/yakuhanjp/ の利用を推奨する
- webfontの`font-face`定義をする場合、weightごとに別々の名前にするのではなく、font-weightとあわせて定義する
- webfontを利用するときは、woff2, woffの優先順位で指定する(アセット通信量削減のため)
- webfontを利用するときは、日本語についてはサブセット配信サービスの利用を強く推奨する(日本語フォントは、常用漢字でサブセット化しても、1ウェイトあたり2-3MBの容量になってしまう。頻繁にアクセスするアプリケーションでない限りは、日本語フォントの自前埋め込みは推奨しない)


例)

```css
@font-face {
  font-family: "YakuHanJP";
  font-style: normal;
  font-weight: 100;
  src: url($theme-path + "fonts/YakuHanJP-Thin.woff2") format("woff2"),
  url($theme-path + "fonts/YakuHanJP-Thin.woff") format("woff");
}

@font-face {
  font-family: "YakuHanJP";
  font-style: normal;
  font-weight: 200;
  src: url($theme-path + "fonts/YakuHanJP-Light.woff2") format("woff2"),
  url($theme-path + "fonts/YakuHanJP-Light.woff") format("woff");
}
```

### 3.2.11 - リセット CSS

* 必ずしもすべてのエレメントをリセットする必要はないが、デザインを実装する際にブラウザ毎の独自の描画を排除できるため、上手に活用することを推奨する。
* ワイルドカードによる全エレメントのリセットはアクセシビリティを低下する恐れがあるため推奨しない。