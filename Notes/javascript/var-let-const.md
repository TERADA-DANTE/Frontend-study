# var vs let vs const

全部変数を宣言するキーワードという共通点がるが、`let`と`const`は ES2015(ES6)から登場し、色んな特徴を持つ。

## スコープ

-   `var`は関数スコープ。
-   `let`と `const`はブロックスコープ。

```javascript
function run() {
    var foo = 'Foo'
    let bar = 'Bar'

    console.log(foo, bar)

    {
        let baz = 'Bazz'
        console.log(baz)
    }

    console.log(baz) // ReferenceError
}

run()
```

<br>

## Hoisting

-   `var`は **関数スコープの最上段に Hoisting され**、宣言の時 `undefined` となる。
-   `let`と `const` は**ブロックスコープの最上段に Hoisting され** 宣言だけされ、値が与えられる前にはなんの値を持たない。

```javascript
function run() {
    console.log(foo) // undefined
    var foo = 'Foo'
    console.log(foo) // Foo
}

run()
```

```javascript
function checkHoisting() {
    console.log(foo) // ReferenceError
    let foo = 'Foo'
    console.log(foo) // Foo
}

checkHoisting()
```

`let`の場合宣言前に Hoisting されるが、どんな値ももたないため ReferenceError が発生する。これを**TDZ(Temporal Dead Zone)**という。

<br>

## Global object

**strict mode 以外**

`var`は global scope で宣言された時 global object に Binding されるが、`let`, `const`は Binding されない。

```javascript
var foo = 'Foo' // globally scoped
let bar = 'Bar' // globally scoped

console.log(window.foo) // Foo
console.log(window.bar) // undefined
```

<br>

## 再宣言 (Redeclaration)

-   `var`は 再宣言が可。
-   `let`と `const`は不可

```javascript
var foo = 'foo1'
var foo = 'foo2' // 問題ない。

let bar = 'bar1'
let bar = 'bar2' // SyntaxError: Identifier 'bar' has already been declared
```

<br>

## let vs const

-   var と let は変更可
-   const は宣言と同時に初期化が行われるため、変更が不可。

<br>

## Reference

-   [Stackoverflow, What's the difference between using “let” and “var”?](https://stackoverflow.com/questions/762011/whats-the-difference-between-using-let-and-var)
-   [Stackoverflow, Are variables declared with let or const not hoisted in ES6?](https://stackoverflow.com/questions/31219420/are-variables-declared-with-let-or-const-not-hoisted-in-es6)
-   [PoiemaWeb, let, const](https://poiemaweb.com/es6-block-scope)
