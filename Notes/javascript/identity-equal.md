# == vs ===

どちらも等しいかを聞く比較を行う。ただ`===`の場合厳密な比較を行い、**Type conversion が行われないため、Type まで一致を確認する。**

```javascript
'' == '0' // false
0 == '' // true
0 == '0' // true

false == 'false' // false
false == '0' // true

false == undefined // false
false == null // false
null == undefined // true

' \t\r\n ' == 0 // true
```

上の例からいくつかの Type 変換が行われるのが確認できる。

ただ、Object/Array の場合は参照 Type であるため、違いがない。

```javascript
var a = {}
var b = {}

a == b // false
a === b // false

var c = []
var d = []

c == d // false
c === d // false
```

文字列の場合 Object として宣言するときがあるため、時と場合による。

```javascript
var a = 'string'
var b = new String('string')
a == b // true
a === b // false
```

Performance はさほど変わらないので気にするところではないが、強制変換をしない、**安全な Type チェックのために===を使うのが望ましい**

<br>

## Reference

-   [Stackoverflow, Which equals operator (== vs ===) should be used in JavaScript comparisons?](https://stackoverflow.com/questions/359494/which-equals-operator-vs-should-be-used-in-javascript-comparisons)
