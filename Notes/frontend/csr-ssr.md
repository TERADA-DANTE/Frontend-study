# CSR(Client Side Rendering)と SSR(Server Side Rendering)

## SPA と MPA

-   **SPA (Single Page Application)**

一つの HTML File に基づいて Javascript を利用し、動的に画面の Contents を変える方式の Web Application。

-   **MPA (Multiple Page Application)**

User が Page を Request するたびに、Server が Request された UI と Data を HTML として Parsing し見せる方式の Web Application。

伝統的な方式では SPA の使う Rendering 方式は CSR で、MPA の使う Rendering 方式は SSR である。
下記にて各方式の動作原理と長所、短所を述べる。

<br>

## CSR

<img src="../../images/frontend/CSR.png">

[Image from](https://medium.com/@adamzerner/client-side-rendering-vs-server-side-rendering-a32d2cf3bfcc)

CRS では Browser が Server に HTML と Javascript file を Request し、Loading が完了したら User との Interaction によって Javascript を利用し、動的に Rendering する。

### :+1: 長所

-   最初の Loading が終わると、動的に早く Rendering されるため、UX がいい。
-   Server に Request する回数が少ないため、Server の負担が低い。

### :-1: 短所

-   最初に全 Script File の Loading を待たないといけない。

    ✅ Resource をチャンク(Chunk)単位に分離し、Request する時にダウンロードさせる方法で Loading 速度を向上することはできる。だが、根本的な解決ではない。

-   Search Engine Bot の Crolling において弱点がある。

    ✅ Google Bot の場合、Javascript を支援するため問題ない。

    ❌ 他社の Search Engine は Javascript を支援しない場合が多々ある。

<br>

## SSR

<img src="../../images/frontend/SSR.png">

[Image from](https://medium.com/@adamzerner/client-side-rendering-vs-server-side-rendering-a32d2cf3bfcc)

SSR では Browser が Page を Request するたびに該当 Page に関する HTML、CSS、Javascipt file および data をもらい rendering する。

### :+1: 長所

-   初期 Loading が早いため、User が Content を早く見ることができる。
-   Javascript を利用した Rendering でないため、SEO(Search Engine Optimization)に有利。

### :-1: 短所

-   Page を Request するたびに毎回 Reload するため、UX が SPA より悪い。
-   Server に毎回 Request をするため、Server の負担が大きい

<br>

## Reference

-   [Client-Side Rendering versus Server-Side Rendering!](https://altalogy.com/blog/client-side-rendering-vs-server-side-rendering/)
-   [What are Single Page Applications(SPA)?](https://dev.to/kendyl93/what-are-single-page-applications-spa-32bh)
-   [The Benefits of Server Side Rendering Over Client Side Rendering](https://medium.com/walmartlabs/the-benefits-of-server-side-rendering-over-client-side-rendering-5d07ff2cefe8)
