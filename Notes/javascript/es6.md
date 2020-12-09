# ES6 (ES2015) 의 특징들

この文書では重要と思われる ES6 のいくつかの特徴を述べる。

<br>

### Arrow Function

`=>` で使うことができる。
関数と違い `this`が関数 Scope に Binding されない。Lexical scope となるため、自分を囲む Code と同じ`this`を共有する。

```javascript
var odds = evens.map((v) => v + 1)
var nums = evens.map((v, i) => v + i)
var pairs = evens.map((v) => ({ even: v, odd: v + 1 }))

nums.forEach((v) => {
    if (v % 5 === 0) fives.push(v)
})

// Lexical scope : this
var bob = {
    _name: 'Bob',
    _friends: [],
    printFriends() {
        this._friends.forEach((f) => console.log(this._name + ' knows ' + f))
    },
}
```

### クラス(Classes)

ㅔプロトタイプ基盤の Object 志向パターン。継承、constructor、Instance、Method などを支援する。

```javascript
class Polygon {
    constructor(height, width) {
        this.name = 'Polygon'
        this.height = height
        this.width = width
    }
    area() {
        return this.height * this.width
    }
}

class Square extends Polygon {
    constructor(length) {
        super(length, length)
        this.name = 'Square'
    }
}
```

### Object literal

Object literal で Object を作る時 Property 指定がもっと柔軟になった。

```javascript
var obj = {
    // Prototype object指定
    __proto__: theProtoObj,
    // property : valueが同じの場合省略可能
    handler,
    // Method
    toString() {
        // super 呼び出し可能
        return 'd ' + super.toString()
    },
    // Property演算
    ['prop_' + (() => 42)()]: 42,
}
```

### Template String

簡単にいうと、文字列と変数を同時に使うこと。

```javascript
`In JavaScript `\n` is a line-feed.` // 改行
`In JavaScript this is
 not legal.`

// interpolation
var name = 'Bob',
    time = 'today'

`Hello ${name}, how are you ${time}?`
```

### Destructuring

```javascript
const [a, , b] = [1, 2, 3]
const [a, b, ...rest] = [10, 20, 30, 40, 50]

var o = { p: 42, q: true }
var { p, q } = o

var o = { p: 42, q: true }
var { p: foo, q: bar } = o

console.log(p, foo) // 42 42
console.log(q, bar) // true true

function g({ name: x }) {
    console.log(x)
}
g({ name: 5 })
```

### Default value, rest

```javascript
function f(x, y = 12) {
    return x + y
}
f(3) == 15 // true
```

```javascript
function f(x, ...y) {
    // y is array!
    return x * y.length
}
f(3, 'hello', true) == 6 // true
```

```javascript
function f(x, y, z) {
    return x + y + z
}
// ArrayのElementを分解
f(...[1, 2, 3]) == 6 // true
```

### Let + Const

[ここ](https://github.com/TERADA-DANTE/Frontend-study/blob/main/Notes/javascript/var-let-const.md)を参照。

### Iterator + For...Of

Iterator は自分なりのループを定義することで、これを`for...of`を使って確認できる。`[Symbol.iterator]`という Method を定義し、この Method は必ず`next()`を持っている Object を Return する。

```javascript
let fibonacci = {
    [Symbol.iterator]() {
        let pre = 0,
            cur = 1
        return {
            next() {
                ;[pre, cur] = [cur, pre + cur]
                return { done: false, value: cur }
            },
        }
    },
}

for (var n of fibonacci) {
    if (n > 1000) break
    console.log(n)
}
```

### Generator

Iterator を簡単に作ることで`function*` と `yield`を使う。

```javascript
var fibonacci = {
    [Symbol.iterator]: function* () {
        var pre = 0,
            cur = 1
        for (;;) {
            var temp = pre
            pre = cur
            cur += temp
            yield cur
        }
    },
}

for (var n of fibonacci) {
    if (n > 1000) break
    console.log(n)
}
```

### Module

[ここ](https://github.com/TERADA-DANTE/Frontend-study/blob/main/Notes/javascript/module.md)を参照

### Map + Set + WeakMap + WeakSet

新しい Data structure, Weak がつくと GC を許可し、`size` Property を持たない。

```javascript
// Sets
var s = new Set()
s.add('hello').add('goodbye').add('hello')
s.size === 2 // false
s.has('hello') === true // true

// Maps
var m = new Map()
m.set('hello', 42)
m.set(s, 34)
m.get(s) == 34 // true

// Weak Maps
var wm = new WeakMap()
wm.set(s, { extra: 42 })

wm.size === undefined // true

// Weak Sets
var ws = new WeakSet()
ws.add({ data: 42 })
// WeakSetに入ってるObjectはなんの参照ももっていない。
```

### Symbol

[ここ](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Symbol)を参照。

### Number + String + Array + Object の追加 Method

```javascript
Number.isInteger(Infinity) // false
Number.isNaN('NaN') // false

'abcde'.includes('cd') // true
'abc'.repeat(3) // "abcabcabc"

Array.from(document.querySelectorAll('*')) //
Array.of(1, 2, 3) // [1,2,3]
    [(0, 0, 0)].fill(7, 1) // [0,7,7]
    [(1, 2, 3)].find((x) => x == 3) // 3
    [(1, 2, 3)].findIndex((x) => x == 2) // 1
    [(1, 2, 3, 4, 5)].copyWithin(3, 0) // [1, 2, 3, 1, 2]
    [('a', 'b', 'c')].entries() // Iterator [0, "a"], [1,"b"], [2,"c"]
    [('a', 'b', 'c')].keys() // Iterator 0, 1, 2
    [('a', 'b', 'c')].values() // Iterator "a", "b", "c"

Object.assign(Point, { origin: new Point(0, 0) }) // Shallow copy
```

### Promise

非同期処理で未来の完了、失敗の結果を示す Object。

```javascript
function timeout(duration = 0) {
    return new Promise((resolve, reject) => {
        setTimeout(resolve, duration)
    })
}

var p = timeout(1000)
    .then(() => {
        return timeout(2000)
    })
    .then(() => {
        throw new Error('hmm')
    })
    .catch((err) => {
        return Promise.all([timeout(100), timeout(200)])
    })
```

<br>
