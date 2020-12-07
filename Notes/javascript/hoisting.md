# ホイスティング(Hoisting)

> ホイスティングの前に[スコープ](https://github.com/TERADA-DANTE/Frontend-study/blob/main/Notes/javascript/scope.md)を必読。

ホイスティングとは巻き上げという意味で **変数または関数の宣言が最上段に巻きあがって行くこと**を示す。ここで注目するところは**宣言**にある。

Javascript

```javascript
console.log(a)
var a = 2
```

Compiler は Javascript Engine が Interpreting する前に Compile を行うが、上の`var a = 2`を 2 つとして見なす。

1.  `var a`
2.  `a = 2`

`var a` は変数の宣言で、Compile の時処理し、`a = 2` は実行するまでおいておく。したがってこの場合変数ａはホイスティングされ、Console は次のような結果を出す。

Console

```javascript
undefined
```

関数の宣言もホイスティングされる。

Javascript

```javascript
func()
function func() {
    console.log('関数ホイスティング')
}
```

Console

```
関数ホイスティング
```

<br>

## 関数ホイスティングでの注意事項

-   **Function Expression はホイスティングされない**

```javascript
func()
var func = function () {}
```

ここでは関数ホイスティングは発生し、参照はできるので ReferenceError は発生しないが、その値が`undefined`であるため TypeError が発生する。

-   **変数よりは関数が先**

```javascript
func()
var func = function () {
    console.log('変数イスティング')
}
function func() {
    console.log('関数イスティング')
}
```

同名の関数宣言の変数宣言(Function Expression)があるが、関数が優先されるため結果は次のようになる。

```
関数イスティング
```

<br>

## Reference

-   [You don't know JS, Scope and Closures : Chapter 5: The (not so) Secret Lifecycle of Variables](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/scope-closures/ch5.md)
