# this binding

EC(Execution Context)が生成されるたびに this binding が起きる。優先順位は次のようである。

1. `new` の場合該当 Object となる。

```javascript
var name = 'global'
function Func() {
    this.name = 'Func'
    this.print = function f() {
        console.log(this.name)
    }
}
var a = new Func()
a.print() // Func
```

2. `call`, `apply`, `bind` のような Binding を使う時は引数としてもらった Object に Binding される。

```javascript
function func() {
    console.log(this.name)
}

var obj = { name: 'obj name' }
func.call(obj) // obj name
func.apply(obj) // obj name
func.bind(obj) // obj name
```

3. Object の Method で呼び出す時は該当 Object に Binding される。

```javascript
var obj = {
    name: 'obj name',
    print: function p() {
        console.log(this.name)
    },
}
obj.print() // obj name
```

4. その他

-   strict mode: `undefined`
-   以外: Browser は `window`、Node.js は`global`

<br>

## Reference

-   [How does the “this” keyword work?](https://stackoverflow.com/questions/3127429/how-does-the-this-keyword-work)
