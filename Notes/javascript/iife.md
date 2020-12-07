# IIFE (Immediately-Invoked Function Expression)

IIFE は訳すと即時実行関数式。 即ち、2 個の条件がつく。

-   **即時実行する**
-   **表現式である。宣言ではない**

```javascript
(function () {
    console.log('IIFE')
})()
```

実行すると IIFE がすぐ出力される。()で囲むことで IIFE となる。

<br>

## 2 種類形態と Arrow 関数

```javascript
(function () {
    console.log('IIFE')
})()
((function () {
    console.log('IIFE')
})())
```

**単純にスタイルの違い** として見なされる 2 種類の表現と Arrow 関数がある。ES2015(ES6)。

```javascript
(() => console.log('IIFE'))()
```

ただ、この場合次のような表現は不可

```javascript
(() => console.log('IIFE')())
```

<br>

## 使う理輔

IIFE を使う理由は普通、Global Scope を汚染させたくないためである。つまり、変数を Global Scope に宣言することを避けること。

### Closure と Private data

IIFE の中で Closure を作ると private Data を作ることができ、これは外部から接近できない。

```javascript
const getCount = (function () {
    let count = 1
    return function () {
        ++count
        return count
    }
})()

console.log(getCount()) // 2
console.log(getCount()) // 3
```

IIFE の中の匿名関数は Closure となり、変数`count`は private Data で使える。Module がこのような方式に依存する。

### 変数の別称(alias)

同じ Global variable を使う 2 つの Library を使う時、Bug を防ぐために使うことができる。jQuery の場合 `$` という Global variable をもっているが、他の Library が`$`を使う時は次のように問題を解決できる。

```javascript
window.$ = funciton(){}
(function($){...})(jQuery)
```

### Minification を使う Optimization

[UglifyJS](https://github.com/mishoo/UglifyJS2) は Javascript の最小化を使って最適化をする。ここには変数名などを短くするのも含まれている。

```javascript
(function(window, document, undefined) {...})(window, document)
```

上を下のようにし、File の Size を圧縮できる。

```javascript
(function(w, d, u) {...})(window, document)
```

<br>

## Reference

-   [Explain the encapsulated anonymous function syntax](https://stackoverflow.com/questions/1634268/explain-the-encapsulated-anonymous-function-syntax)
-   [What is the practical use of an IIFE with a name?](https://stackoverflow.com/questions/18365801/what-is-the-practical-use-of-an-iife-with-a-name)
-   [Use Cases for JavaScript's IIFEs](https://mariusschulz.com/blog/use-cases-for-javascripts-iifes)
-   [What is the (function() { } )() construct in JavaScript?](https://stackoverflow.com/questions/8228281/what-is-the-function-construct-in-javascript)
