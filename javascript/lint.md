# javascript lint

---

## What is that?

<blockquote style="text-align: left;">
lintとは、主にC言語のソースコードに対し、コンパイラより詳細かつ厳密なチェックを行うプログラムである。<br>
転じて、C言語に限らず、各種言語で書かれた文書に対して文法チェックを行うプログラムも、lintと呼ばれるようになった。<br>
[lint - Wikipedia](https://ja.wikipedia.org/wiki/Lint)
</blockquote>

例えば
- [Another HTML-lint](https://ja.wikipedia.org/wiki/Another_HTML-lint)

---

## JSLint

<http://www.jslint.com/>

- かつての業界標準
- 基本、おっさん一人で開発
- 現在も開発は盛ん
- cui での実行には処理系が必要

---

## JSHint

<http://jshint.com/>

- JSLintのfork
- ちょっと前までの業界標準
- コミュニティベースでの開発
- cui での実行には処理系が必要
- エディタ、IDEのプラグインが充実

---

## Closure Linter

<https://developers.google.com/closure/utilities/>

- Google謹製
- チェック(gjslint)だけでなく、修正(fixjsstyle)も行える
- [Google の Style Guide](https://www.google.co.jp/search?q=Google+JavaScript+Style+Guid://www.google.co.jp/search?q=Google+JavaScript+Style+Guide)を使っているなら良いチョイス
- インストールには python が必要

---

## ESLint

<http://eslint.org/>

- 現在(2016)の業界標準
- cui での実行には処理系が必要
- エディタ、IDEのプラグインが充実

---

## JavaScript Lint 

<http://www.javascriptlint.com/>


- ダウンロードして解凍するだけで使用できる
- リリースは2006年、開発も2014年から止まっている
が、ES5までのチェックなら充分使える

```
$ jsl -process /path/to/target.js
```

---

## 独断と偏見で比較してみた


| lint            | 設定 | 拡張性 | 将来度 |
|-----------------|:----:|:------:|:------:|
| JSLint          | △   |  ×    |  △    |
| JSHint          | △   |  ○    | △     |
| Closure Linter  | △   |  △    |  ○    |
| ESLint          | △   |  ○    |  ○    |
| JavaScript Lint | ○   |  ×    | ×     |



---

## Why use that?

不要な error, warning を無くすことができる

- 自分で書くスクリプトは lint を通すべき
- 慣れないうちは面倒。習慣にする工夫が必要。
  - エディタから呼び出す。保存時に実行。
- 他人が書いたスクリプトは？

---

## inline comments

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

## exclude or ignore 

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

## good practice

- lint -> tidy -> test -> commit
- みんなが幸せになれる？

___

Check out Slideck now!

<https://slideck.io/>
