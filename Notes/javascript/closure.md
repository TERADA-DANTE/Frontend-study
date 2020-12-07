# クロージャ(Closure)

Closure とは **関数が属する Lexical scope を記憶し、関数が Lexical scope の外で実行される時にもそのスコープに接近できるようにしてくれる機能**

```javascript
function outer() {
    var a = 2
    function inner() {
        console.log(a)
    }
    return inner
}

var func = outer()
func() // 2
```

ここで Closure は `inner()` となり `func` に含まれ、どこでも Lexical scope を記憶している。

<br>

## 例

Closure を使う代表的な例

```javascript
function func() {
    for (var i = 1; i < 5; i++) {
        setTimeout(function () {
            console.log(i)
        }, i * 500)
    }
}
func()
// 5 5 5 5
```

Code の意図は 1 から 4 まで間隔をおいて出力することだが 5 が 4 回出力される。

`setTimeout()` を Loop の中で実行すると中の Callback が task queue に積み重なり、Loop が終わると Call Stack に戻り実行される、Callback は Closure であるため、上位スコープの`i`を参照する。`func`のスコープでは 5 まで増加したため、5 が 4 回出力される。

<br>

## 解決

2 種類の解決策がある。

-   **新しい関数スコープを作る**

```javascript
function func() {
    for (var i = 1; i < 5; i++) {
        ;(function (j) {
            setTimeout(function () {
                console.log(j)
            }, j * 500)
        })(i)
    }
}
func() // 1 2 3 4
```

`setTimeout()` を IIFE(Immediately Invoked Function Expression)で囲むと新しいスコープを作るため、後で Callback が`j` を参照する時その時の `i` を覚えている。

-   **ブロックスコープで解決**

```javascript
function func() {
    for (let i = 1; i < 5; i++) {
        setTimeout(function () {
            console.log(i)
        }, i * 500)
    }
}
func() // 1 2 3 4
```

関数スコープではなくブロックスコープをもつ`let`を使用すると`for`文内の新しいスコープを持つため、毎回新しい`i`が宣言され、Closure の Callback が`i`を参照するため、上位スコープを検索する時ブロックスコープで毎回宣言および初期化された`i`を参照することになる。

実際 Closure を使う例は [Stackoverflow](https://stackoverflow.com/a/39045098/11789111)にもある。
