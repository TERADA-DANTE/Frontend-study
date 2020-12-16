# ES9 (ES2018) ~ ES10 (ES2019) の特徴

## ES9 (ES2018)

### async Iterator

従来の Iterator の場合 `next()` Method は `value` と `done` をもつ Object を Return した。これからは Promise Object も Return することができる。

```javascript
const asyncIterator = function () {
  let num = 3
  return {
    next() {
      if (num) {
        return Promise.resolve({
          value: num--,
          done: false,
        })
      } else {
        return Promise.resolve({
          done: true,
        })
      }
    },
  }
}

const iterator = asyncIterator()

(async function () {
  await iterator.next().then(console.log) // { value: 3, done: false }
  await iterator.next().then(console.log) // { value: 2, done: false }
  await iterator.next().then(console.log) // { value: 1, done: false }
  await iterator.next().then(console.log) // { done: true }
})()
```

### Object rest/spread

配列で使われる rest/spread が Object でも使えるようになった。

```javascript
const obj = { one: 1, two: 2, three: 3 }
const { one, ...rest } = obj
const newObj = { ...rest, four: 4 }
console.log(rest, newObj) // { two: 2, three: 3 } { two: 2, three: 3, four: 4 }
```

### `Promise.prototype.finally`

Promise を `then` と `catch` で処理した後、 try-catch のように `finally` を使うことができるようになった。

```javascript
const timeout = () => {
  return new Promise((res) => {
    setTimeout(() => {
      res("Promise 終了")
    }, 1000)
  })
}

timeout()
  .then(console.log)
  .finally(() => console.log("必ず"))
```

<br>

## ES10 (ES2019)

### `Array.prototype.flat()/flatMap()`

配列の Flat 化、もしくは結合の Method、`flat`と`flatMap`は例で理解した方がはやい。

```javascript
const arr = [[1, 2, 3], 4, , 5]

console.log(arr.flat()) // [ 1, 2, 3, 4, 5 ]

console.log(
  arr.flatMap((a) => {
    if (a instanceof Array) {
      return a.length
    } else if (Number.isInteger(a)) {
      return a * 2
    } else {
      return undefined
    }
  })
) // [ 3, 8, 10 ]
```

### `Object.fromEntries()`

`Object.entries` の逆。key/value の配列から Object を生成する。

```javascript
const arr = [
  ["one", 1],
  ["two", 2],
  ["three", 3],
]
console.log(Object.fromEntries(arr)) // { one: 1, two: 2, three: 3 }
```

### `String.prototype.trimStart()/trimEnd()`

従来の `String.prototype.trimLeft/trimRight`があるけど、
`String.prototype.padStart/padEnd` と一致させるために新しく誕生した。

```javascript
const target = "    target    "
console.log(target.trimStart())
console.log(target.trimEnd())
```

```
target
    target
```

### catch の error 引数省略可

catch の error 引数の省略が可能となった。

```javascript
try {
  console.log("try")
} catch {} // try
```

<br>

## Reference

- [ECMAScript-new-feature-list, ES2018](https://github.com/daumann/ECMAScript-new-features-list/blob/master/ES2018.MD)
- [ECMAScript-new-feature-list, ES2019](https://github.com/daumann/ECMAScript-new-features-list/blob/master/ES2019.MD)
