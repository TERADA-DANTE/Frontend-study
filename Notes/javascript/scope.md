# スコープ

> スコープの前に[実行コンテキスト(Execution Context)](https://github.com/TERADA-DANTE/Frontend-study/blob/main/Notes/javascript/execution-context.md)を必読。

スコープとは **Javascript Engine が参照の対象となる識別子(Identifier)を検索する時使用する規定** である。即ち、 変数または関数を呼び出すとき該当する識別子を検索するメカニズムである。

<br>

## Lexical scope

Lexical scope とは**変数または関数/ブロックスコープをどこに作成したかによって決まるスコープ** である。"レクシカル(Lexical)"の名前の由来は Javascript compiler が Code を Token に分けて意味付ける Lexing 段階で該当スコープが確定されるためである。簡単にいうと変数または関数/ブロックがどこに書いてあるのかをみてそのスコープを判断することができる。

<br>

## Scope chain

Scope chain は**現在スコープで識別子を検索するとき上位スコープを連鎖的に探していく方式**を示す。実行コンテキストが生成される時その中には LexicalEnvironment と outer 参照がある。その Outer の参照が上位スコープの LexicalEnvironment を参照するため、これがチェインのように連鎖的に連結される。

スコープチェインは下記のように実行される。

1. 現在実行コンテキストの LexicalEnvironment の中の EnvironmentRecord で識別子を検索する。
2. もしない場合、Outer 参照を基盤にスコープチェインに登っていき、上位スコープの EnvironmentRecord にて識別子を検索する
3. 上の過程を Outer の参照が`null`まで探して続け、探せない場合は Error を起こす。

<br>

## Reference

-   [You don't know JS, Scope and Closures](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/scope-closures/ch1.md)
