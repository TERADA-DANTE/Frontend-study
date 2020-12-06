# Module system: CommonJS, AMD, UMD, ES6

## Module とは?

Module とは**いくつかの機能をする Code が集まっている一つの File**のこと。下記のような目的、利点で使われる。

1. **維持、補修** : 数多い機能が Module 化されていると各機能の依存関係が低い。ゆえ、機能の改善、補修が便利である。

2.**Name space** : Javascript で Global variable は Global space を持つため、Code が長ければ長いほど重なる Name space が増える。しかし、Module は Module だけの Name Space を持つため、この問題を解決できる。

3. **再使用性** : 必要な時 Code を繰り返し作成することなく、呼び出しすることができる。

このような長所を生かすために Module の概念が登場し、Javascript 内では Module を開発するためのあらゆるトライがあった。CommonJS、AMD、UMD そして ES6 がその例である。これらの特徴と使用方法を下記にて述べる。

<br>

## CommonJS

Javascript は本来 Browser での言語であった。自然とこれを克服し、Server side、Desktop App にて使うための努力があった。

CommonJS は Javascript が一般的な言語として使われるために Module の概念を生み出した。下記にて CommonJS 式の Module 化を述べる。

他の Module を使う時は**require**、Module を該当 Scope の外に送る時は**module.exports**を使う方式。Node.js では現在この方式を使っている。

Hello world を出力する関数を持つ Module を`a.js`とする。`b.js`は Module からの関数を使う。

-   `a.js`

```javascript
const printHelloWorld = () => {
    console.log('Hello Wolrd')
}

module.exports = {
    printHelloWorld,
}
```

-   `b.js`

```javascript
const func = require('./a.js') // 同じDir内を仮定
func.printHelloWorld()
```

ここで `module.exports` の `module` は該当 Module の情報をもっている Object である。これは Reserved word(予約語)であるため注意しておくべき。`Module`の中に `id` , `path` , `parent` などの Property があり、肝心な`exports` object をがある。

### exports vs module.exports

`module.exports` ではなく `exports` を使う場合がある。この二つに関しては明確に理解しておいた方がいい。

-   `module.exports` は Empty Object を参照する。
-   `exports` は `module.exports` を参照する。
-   `require` は いつも `module.exports` をもらう.

すなわち最初`module.exports`はからの状態。下記のような状態だと考えられる。

```javascript
const module = {
    exports: {},
}
```

したがって、関数を Module の外に送る場合は下のように 2 種類全部有効である

```javascript
exports.printHelloWorld = printHelloWorld
module.exports = { printHelloWorld }
// 結局RequireはModule.exportがReturnするのをもらう
```

それではなぜこのように 2 種類の方法があるのだろう？
これは`exports`がいつも`module.exports`を参照することに注目する必要がある。`exports`を使うことで直接`module.exports`を修正しなくてもいい。`exports`を使って新しい関数、値を追加したり、一部分だけ修正することができる。

🤔 CSS の Override と似たような部分がある。。。
<br>

## AMD(Asynchronous Module Definition)

CommonJS グループから派生した非同期 Module に関しての標準を標榜するグループが AMD。AMD は CommonJS より Browser side での Module に特化している。

Browser は数多い Module が全部 Loading されるまで待つことができない。AMD は非同期処理からその弱点を克服した。

AMD のスペックを実装した Module Loader は RequireJS がある。下記にて簡単な例をあげる。

-   `index.html`

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <title>Document</title>
    </head>
    <body>
        <script data-main="index.js" src="require.js"></script>
    </body>
</html>
```

`require.js` File を `<script>` Tag にいれ、 `data-main` には `require.js` が Loading された後実行する Javascript File を示す。 すなわち, `require.js` が Loading された途端に `index.js` が実行される構造である。

-   `index.js`

```javascript
require.config({
    baseUrl: '/',
    paths: {
        a: 'a',
        b: 'b',
    },
})

require(['a'], (a) => {
    a.printA()
})
```

`require.config`は非同期処理の設定のところである。基本経路と各 Module の経路を設定する。その後、`require` Method を使い、一番目の引数に該当する Module が Loading されたら、それを`a`としてもらい、その中の`printA()`を実行する。

ややこしい説明になっているが、簡単にいうと依存関係を表示した後、Callback 関数を実行する形となっている。

-   `a.js`

```javascript
define(() => {
    return {
        printA: () => console.log('a'),
    }
})
```

Module a は上のようになっている。そして`define()`を使って定義される。`require()`で依存関係を設定したのように、 Callback が実行されるまえに Loading する Module をここでも決めることができる

<br>

## UMD(Universal Module Definition)

上で述べたように Module の実装方式が CommonJS と AMD と分かれるため、それを統一しようとしたのが UMD である。[公式 UMD](https://github.com/umdjs/umd/blob/master/templates/returnExports.js)をみるとしたのようになっている

```javascript
(function (root, factory) {
    if (typeof define === 'function' && define.amd) {
        // AMD. Register as an anonymous module.
        define([], factory)
    } else if (typeof module === 'object' && module.exports) {
        // Node. Does not work with strict CommonJS, but
        // only CommonJS-like environments that support module.exports,
        // like Node.
        module.exports = factory()
    } else {
        // Browser globals (root is window)
        root.returnExports = factory()
    }
})(typeof self !== 'undefined' ? self : this, function () {
    // Just return a value to define the module export.
    // This example returns an object, but the module
    // can return a function as the exported value.
    return {}
})
```

AMD, CommonJS, Browser 方式の Module を支援するためのもので Code をみると下記の通りである。

-   **AMD**: `define()` が関数で `define.amd` Property を持っている
-   **CommonJS**: `module` が Object で `module.exports` Property を持っている
-   **Browser**: その他

統一する具体的な方法は 2 個の引数をもらう関数を実行することである。
1 番目の引数は root となっている。これは Browser の実装に関係するもので`undefined` なら `this` で そうでなければ `self` , すなわち `window` にする。
2 番目の引数として Empty Object を Return する関数を送る、これによって AMD,CommonJS の Module 概念を両方とも支援することができる。

<br>

## ES6(ES2015) 方式

`import` と `export` を使う私にはこれが一番便利である。しかし全 Browser が支援していないため、Babel の `@babel/plugin-transform-modules-commonjs` を使い変換して使用することができる。

Module A、B があって、 下記にてこれらを `export` 、 `import` する方法を述べる。

-   `moduleA.js`

```javascript
const A = () => {}
export default A
```

-   `moduleB.js`

```javascript
export const B = () => {}
```

-   `index.js`

```javascript
import A from 'moduleA'
import { B } from 'moduleB'
```

ここで注目のポイントは **named export** と **default export** にある。

1. **default export**

    **default export**は一回のみ使える。ゆえ、どんな名前で import してもよい。

export

```javascript
const Auth = () = > { ... }

export default Auth

// export default function(){...} ももちろん可
```

import

```javascript
import Auth from './moduleA'
import NewNameAuth from './moduleA'
```

❌ `var`, `const`, `let` を`export default`の後につけることはできない。

2. **named export**

    File 内でいくつかの変数、クラスなどを export することができる。ただし、import の際に同じ名前が必要となる

export

```javascript
export class MyFirstClass { /* ... */ }
export const MySecondConst { /* ... */ }
```

import

```javascript
import { MyFirstClass, MySecondConst } from './moduleA'
```

✅ 別称(alias)を使い `as` で別の名前で import することが可能。

✅ Wild card(`*`)を使い Module 全部を import することが可能。
<br>

## Reference

-   [JavaScript Modules: A Beginner’s Guide](https://www.freecodecamp.org/news/javascript-modules-a-beginner-s-guide-783f7d7a5fcc/)
-   [module.exports vs exports in Node.js](https://stackoverflow.com/questions/7137397/module-exports-vs-exports-in-node-js)
