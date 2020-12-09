# Strict モード (Strict mode)

ECMAScript5 から導入された機能で **既存の無視されたエラーに対してエラーを発生する。** File 全体に適用することもできるし、関数 Scope に適用できる。ただ、ブロック Scope に適用することはできない。

```javascript
'use strict' // File全体

function f() {
    'use strict' // 関数に適用
}
```

Strict モードを使い、ミスを取ることができ、より安全な Code がかける。例としていくつか下記にて述べる。

-   `var` が省略された変数を Global に Binding しない。
-   `NaN = 5` などは不可能 -　 delete できない Property を削除することはできない。
-   関数の引数の名前は同じくできない。
-   `with` 使用不可
-   変数の削除不可(`delete x`)
-   `arguments.callee` 使用不可
-   `arguments` Object は必ず原本引数を保存する。つまり、parameters を変えても `arguments` は変わらない。
-   0xOCT 使用不可 (`var a = 013`)
-   `eval` は新しい変数をスコープに追加しない（そもそも使わないのが望ましい）

JSLint や ESLint のような Linter を使う場合以外は`"use strict"` が望ましい。

<br>

## Reference

-   [MDN, Strict mode](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Strict_mode)
-   [Stackoverflow, What does “use strict” do in JavaScript, and what is the reasoning behind it?](https://stackoverflow.com/questions/1335851/what-does-use-strict-do-in-javascript-and-what-is-the-reasoning-behind-it)
