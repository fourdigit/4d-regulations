---
title: "Overview"
description: "my description"
layout: "./docs/template/template.pug"
---

[TOC]

# 1 - 全体の設計思想

## 1.1 - HTML、CSS、Javascript の分担

HTML、CSS、Javascript の分担は次のような整理になります：

* HTML：情報構造の定義
* CSS：装飾の定義（アニメーションの定義も含む）
* Javascript：機能の定義

HTML 側に CSS や Javascript を直接記述したり、Javascript で CSS 属性を直接変更してしまうと、予期できない副作用が発生しやすくなります。
CSS in JSは、学習コストの上昇と、受けられる恩恵のトレードオフを考えた際に導入のメリットがあまりないので、Angularのようにフレームワークとして推奨している場合をのぞいて利用しません。

HTML に直接 Javascript を記述する例外は次の通りになります：

* 3rd パーティサービス（analytics や AB テストなど）のタグ

## 1.2 - Atomic Design の設計思想

サイト内のパーツを極力再利用出来るようにする事で、  
メンテ性・拡張性の向上、デバッグのしやすさの向上、サイト規模への依存の低減を図れます。

そのため、ページ特有の機能や装飾は極力ないようにし、  
すべての要素がモジュールのような Atomic Design の設計思想を推奨します。  
また、Atomic DesignとBEMを組み合わせた設計を利用することが社内では多いです(ABEM)
(クライアント指定のネーミングルールがあれば、それを利用してください)

参考）  
[http://getbem.com/](http://getbem.com/)  
[https://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/](https://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)  
[https://www.lullabot.com/articles/bem-atomic-design-a-css-architecture-worth-loving](https://www.lullabot.com/articles/bem-atomic-design-a-css-architecture-worth-loving)
[http://bradfrost.com/blog/post/atomic-web-design/](http://bradfrost.com/blog/post/atomic-web-design/)
[ABEM. A more useful adaptation of BEM.](https://css-tricks.com/abem-useful-adaptation-bem/)

