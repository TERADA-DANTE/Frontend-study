# Module bundler と Transpiler

# Module bundler

> Module の概念がいまいちならこの文書の[Module system](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/javascript/module.md) を先に必読。

最近の Frontend 開発は Module 単位で File を作り開発する方式である。すなわち、Module はお互い依存しあう関係の上にいるため、次のような問題が発生する。

-   数多い Module の順番をどのように処理するか？
-   Module が多くなると HTTP Request, Response が多くなる。これによる Overhead はどのように解決するか？
-   ES6 以上のスペックの Code をどのように処理するか？

上の問題を解決するために登場したのが**Module Bundler**である。
各々の Module の依存性を解決し、一つの Javascript にする同時に ES6 以上のスペックを ES5 に変換するツール。

画像圧縮、最小化(Minification)など色んな機能を提供し、有名な Bundler には Webpack、Parcel、Rollup がある。

<br>

## Transpiler

トランスパイリング(Transpiling)とは**A の言語で作成された Code を似たような B 言語に変換する行為**であり、これをしてくれるのがトランスパイラー(Transpiler)である。

Transpiler が必要な理由は全 Browser が ES6 以上の機能を支援してないので ES5 Code に変換するのが要求されるためである。実際以外にも React.js の JSX を Javascript に変換したり、TypeScript を Javascript に変換する役割も担当している。ES6+や JSX の Transpiler には有名な Babel がある。

普通 Frontend Framework, Library を使用し開発する時は Module Bundler に Transpiler を追加している。

<br>

## Reference

-   [What is module bundler and how does it work?](https://dev.to/tanhauhau/what-is-module-bundler-and-how-does-it-work-3gp2)
