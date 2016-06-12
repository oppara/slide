
# javascript tools

- bin: 処理系
- lint: 文法チェッカ
- tidy: 整形ツール

<!-- 
- test: TDD/BDD
- doc: APIドキュメント生成
- task runner: 

http://qiita.com/gitseitanaka/items/0a465f36281519846141
https://ics.media/entry/6789
-->

---

## bin: What is that?

- JavaScript( or ECMAScript) を実行する処理系
- ウィンドウのないWEBブラウザ？
- 単体では DOM のようなホスト環境は提供しない。
  - `document.xxx();` とかは出来ない

---

## bin: SpiderMonkey

[SpiderMonkey](https://developer.mozilla.org/ja/docs/SpiderMonkey)

- Mozilla による C/C++ の実装
- すべての始まり
- 1996年3月 Netscape Navigator 2.0
- Mozilla Firefox, Adobe Acrobat, Yahoo! Widget 等

---

## bin: Rhino

[Rhino](https://developer.mozilla.org/ja/docs/Rhino)

- Mozilla が管理する Java(JVM) 上の実装
- 1997年より開発開始
- Java から JavaScript の関数を呼べる。その逆も可。
- Server-Side JavaScriptの走り。<span class="fragment" data-fragment-index="1">走ったっけ？</span>
- OpenOffice, J2SE 6 等

  
---

## bin: Google V8 JavaScript Engine

[Google V8 JavaScript Engine](https://developers.google.com/v8/)

- Google が開発する C++ の実装
- 2008年より開発開始
- Google Chrome, Node.js

---

## bin: PhantomJS

[PhantomJS](http://phantomjs.org/)

- JavaScript API を備えた Headless な WebKit(QtWebKit) ベースのブラウザ
- ぶっちゃけ、[QtWeb](http://www.qtweb.net/) からウィンドウを取払ったもの
  - DOM あります
  - Canvas あります

---

## bin: jsc

[JavaScriptCore.framework (jsc)](http://developer.apple.com/library/mac/#documentation/Carbon/Reference/WebKit_JavaScriptCore_Ref/)

Mac の場合、デフォルトで入ってたりします

- WebKit に JavaScript Engine を提供する framework
- osx 10.5 から

```
$ /System/Library/Frameworks/JavaScriptCore.framework/Versions/A/Resources/jsc -h
```

---

## bin: Why use that?

<ul>
<li>コマンドラインから JavaScript が実行できる</li>
<li class="fragment" data-fragment-index="1">エディタから呼び出せる</li>
<li class="fragment" data-fragment-index="1">テストに使える！</li>
<li class="fragment" data-fragment-index="2">俺かっけー</li>
</ul>

---

## lint: What is that?

<blockquote style="text-align: left;">
lintとは、主にC言語のソースコードに対し、コンパイラより詳細かつ厳密なチェックを行うプログラムである。<br>
転じて、C言語に限らず、各種言語で書かれた文書に対して文法チェックを行うプログラムも、lintと呼ばれるようになった。<br>
[lint - Wikipedia](https://ja.wikipedia.org/wiki/Lint)
</blockquote>

例えば
- [Another HTML-lint](https://ja.wikipedia.org/wiki/Another_HTML-lint)


---

## lint: JSLint

[JSLint](http://www.jslint.com/)

- かつての業界標準
- 基本、おっさん一人で開発
- 現在も開発は盛ん
- cui での実行には処理系が必要

---

## lint: JSHint

[JSHint](http://jshint.com/)

- JSLintのfork
- ちょっと前までの業界標準
- コミュニティベースでの開発
- cui での実行には処理系が必要
- エディタ、IDEのプラグインが充実

---

## lint: Closure Linter

[Closure Linter](https://developers.google.com/closure/utilities/)

- Google謹製
- チェック(gjslint)だけでなく、修正(fixjsstyle)も行える
- [Google の Style Guide](https://www.google.co.jp/search?q=Google+JavaScript+Style+Guid://www.google.co.jp/search?q=Google+JavaScript+Style+Guide)を使っているなら良いチョイス
- インストールには python が必要

---

## lint: ESLint

[ESLint](http://eslint.org/)

- 現在(2016)の業界標準
- cui での実行には処理系が必要
- エディタ、IDEのプラグインが充実

---

## lint: JavaScript Lint 

[JavaScript Lint ](http://www.javascriptlint.com/)


- ダウンロードして解凍するだけで使用できる
- リリースは2006年、開発も2014年から止まっている
が、ES5までのチェックなら充分使える

```
$ jsl -process /path/to/target.js
```

---

## lint: Why use that?

不要な error, warning を無くすことができる

- 自分で書くスクリプトは lint を通すべき
- 慣れないうちは面倒。習慣にする工夫が必要。
  - エディタから呼び出す。保存時に実行。
- 他人が書いたスクリプトは？

---

## lint: inline comments

一部分を lint 対象からはずすことができる

```javascript
/* jshint ignore:start*/
  (code that fires warnings)
/* jshint ignore:end */

// eslint-disable-next-line no-use-before-define
  (code that fires warnings)

/*eslint-disable */
  (code that fires warnings)
/*eslint-enable */

/*jsl:ignore*/
  (code that fires warnings)
/*jsl:end*/
```
---

## lint: exclude or ignore 

無視するファイルを指定する

```
$ jshint --exclude 'node_modules/*' .
$ jshint --exclude-path /path/to/.jshintignore .

$ eslint --ignore-pattern '/lib/' --ignore-pattern '/src/vendor/*' .
$ eslint --ignore-path /path/to/.eslintignore .
$ cat .eslintignore
node_modules/*
**/vendor/*.js
```

---

## tidy: What is that?

<blockquote style="text-align: left;">
整える、整理する、整頓する、片付ける、身繕いする<br>
[英辞郎 on the WEB：スペースアルク](http://eow.alc.co.jp/tidy/UTF-8/)
</blockquote>


例えば
- [HTML Tidy](http://www.html-tidy.org/)
- [Perltidy](http://perltidy.sourceforge.net/)

---

## tidy: js-beautify

[js-beautify](http://jsbeautifier.org/)

<p>Beautify, unpack or deobfuscate JavaScript.</p>

- bookmarklet、ブラウザの機能拡張が充実
- エディタ、IDEのプラグインが充実
- cui での実行には処理系が必要

---

## good practice

- lint => tidy => test => commit
- みんなが幸せになれる？

---

Check out Slideck now!

<https://slideck.io/>
