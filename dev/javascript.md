---
title: "JavaScript"
description: "my description"
layout: "./docs/template/template.pug"
---

[TOC]

# 4 - JavaScript

## 4.1 - 設計

### 4.1.1 - モジュールバンドラの利用

直接JSを編集する(お客さん側, BE側で触る)というケースでない限りは、webpackなどのモジュールバンドラ利用を推奨します。


### 4.1.2 - 要素や変数が無いケースを考慮した実装

画面によって要素が存在しなかったり、変数が未定義であったりする場合がないか考え、要素や変数がないかも知れない前提で実装してください

例)

```javascript
function initModuleA($el) {
  if(!$el[0]) return null;
  $el.on("click", function(e) {
    ...
  });
}

$(".o-modulea").each(function(el) {
  initModuleA($(el));
});
```

### 4.1.3 - 推奨ライブラリ

| 用途                   | 推奨ライブラリ | 特徴                                                                                                                                                                                 | 取得先                                                                                       |
| ---------------------- | -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------- |
| 配列やオブジェクト操作 | lodash         | 複雑な配列操作(ソート、グループ化)を簡単におこなえる。なお、`map`, `reduce`, `some`, `forEach`などは2019年時点で対象となる全てのブラウザでネイティブ実行できるので、ネイティブのものをつかうこと。webpackでよびだすときは`lodash-webpack-plugin`を利用すること。           | [https://lodash.com/](https://lodash.com/)                                                   |
| カルーセル             | swiper         | ・高いカスタマイズ性 ・モバイル対応                                                                                          | [http://idangero.us/swiper/](http://idangero.us/swiper/)                                     |
| promise                | bluebird       | IE11でPromiseを利用できる。                  | [http://bluebirdjs.com/](http://bluebirdjs.com/)                                             |
| 時間表示操作           | day.js or date-fns | ・ローカライゼーションされている・時間の操作も出来る・moment.jsよりバンドルサイズが軽い                                                                                                                               | [https://momentjs.com/](https://momentjs.com/)                                               |
| 数値表示操作           | numeral.js     | ・API が moment.js に似ていて使いやすい                                                                                                                                              | [http://numeraljs.com/](http://numeraljs.com/)                                               |
| クッキー操作           | js-cookie      |                                                                                                                                                                                      | [https://github.com/js-cookie/js-cookie](https://github.com/js-cookie/js-cookie)             |
| url parser             | url-parse      |                                                                                                                                                                                      | [https://github.com/unshiftio/url-parse](https://github.com/unshiftio/url-parse)             |
| デバイス判別           | current-device | ・デバイス、ブラウザの種類、画面の向きを簡単に判別できる・HTML 要素の class 属性にデバイス、ブラウザの種類、画面の向き情報を挿入するため、CSS で扱いやすい・ライブラリサイズが小さい | [https://thematthewhudson.com/current-device/](https://thematthewhudson.com/current-device/) |
| ブラウザ判別           | bowser         | ・useragent をパースせずにブラウザ情報を規則的に取得できる・幅広いブラウザの数を判別できる・ブラウザのバージョンまで取得できる                                                       | [https://github.com/lancedikson/bowser](https://github.com/lancedikson/bowser)               |

※ ライブラリを選定する際には、レポジトリのの更新頻度や浸透度合い（star 数、npm の DL 数）を参考にしています。

### 4.1.4 - 命名規則

変数や関数名は camel case で指定します。定数は大文字の「\_」区切りで指定し、変数と定数を区別出来るようにします。

### 4.1.5 - LINT

JavaScript の記述フォーマットをプロジェクト内で統一するために「eslint」を使用しています。  
ルールは`/.eslintrc`ファイルに記述しています。  
ルールが、FOURDIGIT内のプロジェクトごとや個人ごとにばらつくのを防ぐため、eslint を package 化しました。  
下記より、READMEを参照し導入してください。  
[https://github.com/fourdigit/eslint-config-fourdigit](https://github.com/fourdigit/eslint-config-fourdigit)  

※ 各種ルールについては eslint のルールリファレンスを参照ください。  
[https://eslint.org/docs/rules/](https://eslint.org/docs/rules/)  
※ vendor の JavaScript は lint 対象外していています。  
※ lint から ignore したいファイルや行がある場合は、仕様統制者と事前に確認して行ってください。

### 4.1.6 - コーディングガイドライン

Airbnb の Javascript スタイルガイドに一般的な  
[https://github.com/airbnb/javascript](https://github.com/airbnb/javascript)

## 4.2 - ベストプラクティス

### 4.2.1 - SessionStorage／LocalStorage／Cookie などの参照

各種機能から LocalStorage や Cookie などの直接参照は極力避けることを推奨します。  
SessionStorage や LocalStorage や Cookie をラッピングする共通機能を作成したり、npmから読み込むことで、その機能内で状態を管理する事で、ブラウザの仕様による差など吸収する事が出来ます。

### 4.2.2 - jQuery を使う際の注意点

#### $変数名

jQuery 要素と素 html 要素を区別しやすくするため、
jQuery 要素の変数名の先頭に「$」をつける事を推奨します。 (`eslint-plugin-dollar-sign` で制約をかけることをさらに推奨します)

```javascript
var $button = $(.button);

$(".someclass").each(function(el) {
  ...
});
```

#### Selector の使用を削減

`$("")`の要素検索の実行が多いと、性能への影響がでる可能性があります。一度検索かけたものは変数に保持したり、コマンドをチェーンさせて実行を減らす事を推奨します。  
 例）

```javascript
var $button = $("button");
$button.addClass("someclass");
$button.on("click", function(e) { … });

$button
  .addClass("someclass")
  .removeClass("otherclass")
  .text("clicked");
```

#### domready

jQuery の domready は文は次のものに統一します。

```javascript
$(function() {
  ...
});
```

#### domready vs document onload

domready は DOM が読み込まれた時点で発火します。  
 → ページの機能付与はこの時点で実施。  
 document onload はページの初期ロードが完了した時点で発火します。  
 → ページロードが完了しないと取得できない情報（ページの px 数での長さなど）を取得したい時のみに使います。  
 また、domready 内に document onload を記述しますと、ブラウザによって発火しないケースもあるため、別々で記述します。

```javascript
  // NGパターン
  $(function() {
    $(document).on("load", function(e) {
      ...
    });
  });

  // 正しいパターン
  $(function() {
    …
  });
  $(document).on("load", function(e) {
    ...
  });
```

## jQueryを使う場合
jQueryはいろいろできるのですが、次の使用に次の機能のみの使用を推奨します。アニメーションなどはv3系になって`requestAnimationFrame`が使われるようになり多少速度は改善していますが、CSS animationや他のJSライブラリのほうがカクつきを防ぎ易いです。

- DOM ready: `$(function() { ... });`
- ajax通信：`$.ajax()`
- DOM 要素取得*：`$("selector")`、`$element.find("selector")`
- DOM操作*：`append()`、`remove()`
- クラス・スタイル操作*：`addClass()`、`removeClass()`、`css()`
- イベント操作*：`on()`、`off()`

### jQuery の拡張を書く場合

下記のようなコードで jQuery の拡張機能を作成する場合は、アプリーケーションのコードに混在させず、他の vendor 系 jQuery 拡張を同様に `jquery.somefunctionname.js` のようなファイルを作成し、`/common/js/vendor/`などに格納する事を推奨します。

```javascript
  $.fn.somefunc = function() {
    …
  };
```
