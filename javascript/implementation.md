# JavaScript Implementation 

処理系の話

<!-- 
- test: TDD/BDD
- doc: APIドキュメント生成
- task runner: 

http://qiita.com/gitseitanaka/items/0a465f36281519846141
https://ics.media/entry/6789
-->

---

## What is that?

- JavaScript (or ECMAScript) を実行するプログラム
<li class="fragment" data-fragment-index="1">ウィンドウのないWEBブラウザ？</li>
<li class="fragment" data-fragment-index="2">単体では DOM のようなホスト環境は提供しない</li>
<li class="fragment" data-fragment-index="3">`document.xxx();` とかは出来ない</li>

---

## SpiderMonkey

<https://developer.mozilla.org/ja/docs/SpiderMonkey>

- Mozilla による C/C++ の実装
- すべての始まり
- 1996年3月 Netscape Navigator 2.0
- Mozilla Firefox, Adobe Acrobat, Yahoo! Widget 等

```
$ brew update && brew install sidermonkey
$ js
js> [1,2,3,4,5].map(function(n) {return n * n})
js> help() 
js> quit()
```
---

## Rhino

<https://developer.mozilla.org/ja/docs/Rhino>

- Mozilla が管理する Java(JVM) 上の実装
- 1997年より開発開始
- Java から JavaScript の関数を呼べる。その逆も可。
- Server-Side JavaScriptの走り。<span style="font-size: small" class="fragment" data-fragment-index="1">走ったっけ？</span>
- OpenOffice, J2SE 6 等

```
$ brew update && brew install rhino 
$ rhino
js> [1,2,3,4,5].map(function(n) {return n * n})
js> help() 
js> quit()
```

---

## Google V8 JavaScript Engine

<https://developers.google.com/v8/>

- Google が開発する C++ の実装
- 2008年より開発開始
- Google Chrome, [Node.js](https://nodejs.org/)

```
$ brew update && brew install node
$ node
> [1,2,3,4,5].map(function(n) {return n * n})
> .help
> .exit
```
---

## PhantomJS

<http://phantomjs.org/>

- JavaScript API を備えた Headless な WebKit(QtWebKit) ベースのブラウザ
- ぶっちゃけ、[QtWeb](http://www.qtweb.net/) からウィンドウを取払ったもの
  - DOM あります
  - Canvas あります

```
$ brew update && brew install phantomjs
$ phantomjs
phantomjs> [1,2,3,4,5].map(function(n) {return n * n})
phantomjs> phantom.exit()
```

---

## JavaScriptCore.framework (jsc)

<https://developer.apple.com/library/tvos/documentation/Carbon/Reference/WebKit_JavaScriptCore_Ref/index.html>

Mac の場合、デフォルトで入ってたりします

- Xcode プロジェクトに JavaScriptCore.framework を追加する
- osx 10.5 から

```
$ alias jsc="/System/Library/Frameworks/JavaScriptCore.framework/Versions/A/Resources/jsc"
$ jsc
>>> [1,2,3,4,5].map(function(n) {return n * n})

Type ctrl-c to exit the REPL.
```

---

## Why use that?

<ul>
<li>コマンドラインから JavaScript が実行できる</li>
<li class="fragment" data-fragment-index="1">テストに使える！</li>
<li class="fragment" data-fragment-index="2">エディタから呼び出せる！！</li>
<li class="fragment" data-fragment-index="3">俺かっけー</li>
</ul>

---

## good practice

- lint -> tidy -> test -> commit
- みんなが幸せになれる？

___

Check out Slideck now!

<https://slideck.io/>
