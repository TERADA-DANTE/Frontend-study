# Frontend-study

フロントエンドエンジニアとしての基礎知識

## 目次

1.  [紹介](#tada-紹介)
2.  [Frontend 全般](#computer-Frontend-全般)
3.  [HTML](#page_with_curl-html)
4.  [CSS](#lipstick-css)
5.  [Javascript](#fire-javascript)
6.  [Network](#chart_with_upwards_trend-Network)
7.  [Security](#lock-Security)

## :tada: 紹介

フロントエンドエンジニアとして**必ず**知っておくべきの知識をまとめました。実際の面接質問や大学時代の知識を整理しました。

-   基礎知識を浅すぎないように、深すぎないように**ある程度** 整理しました。
-   パソコン工学の全般ではありません。**フロントエンドのみ** です。
-   個人的に作成した資料であります。**間違える恐れがあります**。PR、ISSUE をいつもお待ちしております。

## :computer: Frontend 全般

-   [CSR (Client Side Rendering) vs SSR(Server Side Rendering)](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/frontend/csr-ssr.md)
-   [Browser の Rendering 過程](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/frontend/browser-rendering.md)
-   [Javascript engine が Code を実行する過程](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/frontend/engine.md)
-   [BOM と DOM](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/frontend/bom-dom.md)
-   [Module bundler と Transpiler](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/frontend/bundler-transpiler.md)
-   [CI と CD](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/frontend/ci-cd.md)

## :page_with_curl: HTML

-   [DOCTYPE](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/html/doctype.md)

-   [標準モードと互換モード](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/html/standard-quirks.md)

-   [data- 属性](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/html/data.md)

-   [local storage vs session storage vs cookie](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/html/web-storage-api.md)

-   [script vs script async vs script defer](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/html/script-tag-type.md)

-   [Semantic markup](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/html/semantic.md)

## :lipstick: CSS

-   [Box Model](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/css/box-model.md)

-   [float を解除する方法](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/css/float-clear.md)

-   [margin が重なる場合(Margin-Collpasing)](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/css/margin-collapsing.md)

-   [BFC (Block Formatting Context)](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/css/bfc.md)

-   [z-index の原理](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/css/z-index.md)

-   [block vs inline vs inline-block](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/css/block-inline-inline-block.md)

-   [横/縦真ん中に整列](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/css/center.md)

-   [Reset.css vs Normalize.css](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/css/reset-normalize.md)

-   [Grid system](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/css/grid.md)

-   [img の下の空白](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/css/img-space.md)

## :fire: Javascript

-   [AJAX](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/javascript/ajax.md)

-   [イベント委任 (Event Delegation)](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/javascript/event-delegation.md)

-   [実行コンテキスト(Execution Context)](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/javascript/execution-context.md)

-   [スコープ (Scope)](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/javascript/scope.md)

-   [ホイスティング (Hoisting)](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/javascript/hoisting.md)

-   [クロージャ (Closure)](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/javascript/closure.md)

-   [Native object vs Host object](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/javascript/native-host.md)

-   [this binding](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/javascript/this.md)

-   [var vs let vs const](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/javascript/var-let-const.md)
<!--
-   [IIFE (Immediately-Invoked Function Expression)](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/javascript/iife.md) -->

-   [Module system: CommonJS, AMD, UMD, ES6](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/javascript/module.md)
<!-- -   [콜 스택(Call stack)과 힙(Heap)](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/javascript/stack-heap.md)
-   [이벤트 루프 (Event loop)](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/javascript/event-loop.md)
-   [프로토타입 (Prototype)](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/javascript/prototype.md)
-   [== vs ===](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/javascript/identity-equal.md)
-   [엄격 모드 (Strict mode)](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/javascript/strict-mode.md)
-   [new의 동작방식](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/javascript/new.md)
-   [ES6 (2015) 의 특징들](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/javascript/es6.md)
-   [ES7 (ES2016) ~ ES8 (ES2017) 의 특징들](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/javascript/es7-es8.md)
-   [ES9 (ES2018) ~ ES10 (ES2019) 의 특징들](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/javascript/es9-es10.md)
-   [ES11 (ES2020) 의 특징들](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/javascript/es11.md) -->

## :chart_with_upwards_trend: Network

-   [TCP と UDP](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/network/tcp-udp.md)

-   [HTTP](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/network/http.md)
<!--
-   [HTTPS](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/network/https.md)
-   [URL과 URN을 포함하는 URI](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/network/uri.md)
-   [REST API](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/network/rest-api.md)
-   [Cookie vs Session](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/network/cookie-session.md)
-   [URL을 입력하고 벌어지는 일](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/network/type-url-process.md) -->

## :lock: Security

-   [CORS(Same Origin Policy)](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/security/sop.md)
<!-- * [XSS와 CSRF](https://github.com/TERADA-DANTE/Frontend-study/blob/master/Notes/security/xss-csrf.md) -->
