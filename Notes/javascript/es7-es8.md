# ES7 (ES2016) ~ ES8 (ES2017) の特徴

## ES7 (ES2016)

### `Array.prototype.includes`

- `arr.includes(元素, [, Indexの始まり])`

配列の中に元素が入っているかを確認する Method

```javascript
[1, 2, 3].includes(2) // true
[1, 2, NaN].includes(NaN) // true
[1, 2, 3].includes(2, 2) // false
[1, 2, 3].includes(3, 4) // index範囲外なので false
```

### Exponentiation

- `n ** m`

Python と一緒。

```javascript
2 ** 2 // 4
Math.pow(2, 2) // 4
```

<br>

## ES8 (ES2017)

### `async - await`

- `async function 関数名 (args...) {}`

非同期関数をより直観的に使うことができるようになった。

`async`関数内の`await`は Promise の完了を待つ。

```javascript
const promiseFunc1 = function () {
  return new Promise((res, rej) => {
    setTimeout(() => {
      res("1番 Promise")
    }, 1000)
  })
}

const promiseFunc2 = function () {
  return new Promise((res, rej) => {
    setTimeout(() => {
      res("2番 Promise")
    }, 1000)
  })
}

const handleAsyncFunc = async function () {
  const promiseMessage1 = await promiseFunc1()
  const promiseMessage2 = await promiseFunc2()
  console.log(promiseMessage1, promiseMessage2)
}

handleAsyncFunc() // 1番 Promise 2番 Promise
```

### `Object.entries()`

- `Object.entries(オブジェクト))`

key/value を配列に変換する Method

```javascript
const obj = { one: 1, two: 2, three: 3 }
console.log(Object.entries(obj))
// [['one', 1], ['two', 2], ['three', 3]]
```

### `Object.values()`

- `Object.values(オブジェクト)`

オブジェクトの value のみ配列に変換する

```javascript
const obj = { one: 1, two: 2, three: 3 }
console.log(Object.values(obj))
// [1, 2, 3]
```

### `Object.getOwnPropertyDescriptors()`

- `Object.getOwnPropertyDescriptors(オブジェクト)`

Property の Discriptor である `value`, `writable`, `enumerable`, `configurable`, `set`, `get`を持ってくる Method

```javascript
const obj = { one: 1, two: 2, three: 3 }
console.log(Object.getOwnPropertyDescriptors(obj))
```

```
{
  one: { value: 1, writable: true, enumerable: true, configurable: true },
  two: { value: 2, writable: true, enumerable: true, configurable: true },
  three: { value: 3, writable: true, enumerable: true, configurable: true }
}
```

<br>

## Reference

- [ECMAScript-new-feature-list, ES2016](https://github.com/daumann/ECMAScript-new-features-list/blob/master/ES2016.MD)
- [ECMAScript-new-feature-list, ES2017](https://github.com/daumann/ECMAScript-new-features-list/blob/master/ES2017.MD)
