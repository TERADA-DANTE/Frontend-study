# 実行コンテキスト (Execution Context)

実行コンテキストとは**Code の実行環境に関して色んな情報をもっている概念**であり、簡単にいうと Javascript Engine で作られ、使われる Code の情報を持っている Object の Set である。

<br>

## 種類

Javascript の Code は 3 種類で分けられて、Global scope で実行される Global code、 function scope で実行される function code、そして`eval()`で実行されるコードがある。この三つの Code は各々の Execution context を生成する。

Javascript Engine が Script を実行する前に**Global Execution Context, GEC**が作られ、関数を呼び出すたびに**Function Execution Context, FEC**が作られる。ここで重要なのは Global の場合実行する前であるが、関数の場合呼び出しの時に作られるのである。

<br>

## Execution Context Stack

Execution Context が作られるとこれは **コールスタック(Call Stack)** と言われる Execution Context Stack に積み重なる。GEC は Code を実行するまえに積み重なり、全 Code を実行するとなくなる。FEC は呼び出しの時に積み重なり、呼び出しが終わると削除される。下記にて説明を続ける。

```javascript
function func() {
    console.log('関数実行コンテキスト')
}
console.log('グローバル実行コンテキスト')
func()
```

最初に Code を実行する前に GEC が積み重なり、Code を実行すると Console には`グローバル 実行コンテキスト`が出力される。その後、`func()`を呼び出すと該当 FEC が作られ、積み重なり、Console には`関数実行コンテキスト`が出力される。以降 FEC がスタックから削除され、全 Code の実行が終わったら GEC がスタックから削除される。

![GIF](https://miro.medium.com/max/1100/1*dUl6qPEaDJJTXWythQsEtQ.gif)

<br>

## 構造

Execution Context は次のような構造要素を持っている。

-   Lexical Environment
-   Variable Environment
-   this Binding

### Lexical Environment

Lexical Environment は**変数および関数などの識別子(Identifier)、外部参照に関しての情報を持っている Component**である。この Component は 2 個の要素を更に持つ。

-   **Environment Record**
-   **outer 参照**

Environment Record が識別子に関しての情報を持ち、outer 参照は外部 Lexical Environment を参照する Pointer である。

Javascript

```javascript
var x = 10

function foo() {
    var y = 20
    console.log(x)
}
```

上のような Code は下のような Lexical Environment を生成する。

```javascript
globalEnvironment = {
	environmentRecord = { x: 10 },
	outer: null
}
fooEnvironment = {
	environmentRecord = { y: 20 },
	outer: globalEnvironment
}
```

したがって、`foo()` で `x`を参照するとまずは該当 Environment Record を確認し、ない場合 Outer 参照を使い外部の Lexical Environment に属する Environment Record を探す過程を行う。

### Variable Environment

Variable Environment は Lexical Environment と同じ性格を帯びるが、**`var` で宣言された変数のみ保存する**。 すなわち、Lexical Environment는 `var` 以外の(`let` 、関数など)を保存する ( 明確な Code は [ここで](https://stackoverflow.com/a/45788048/11789111) 確認できる )

### this Binding

`this`の Binding は Execution Context が作られる時に`this`にどのように Binding されるのかを示す。

-   **GEC の場合**
    -   strict mode の場合は `undefined` として Binding される。
    -   以外は Global object として Binding される。(Browser は `window`, Node.js では `global`)
-   **FEC の場合**
    -   該当関数の呼び出しによる。

<br>

## Execution Context の過程

Execution Context の過程は 2 段階に分かれる。

1. **Creation Phase (生成)**
2. **Execution Phase (実行)**

### Creation Phase

Creation Phase さらに 3 段階に分かれる。

1. Lexical Environment 生成
2. Variable Environment 生成
3. this Binding

ここでは**値が変数に Mapping されない**。 `var` は `undefined`、`let` や `const`はまだなんの値も持っていない状態。

### Execution Phase

Code を実行しながら**値を変数に Mapping させる**

```javascript
var a = 3
let b = 4

function func(num) {
    var t = 9
    console.log(a + b + num + t)
}

var r = func(4)
```

下記にて GEC,FEC の生成と実行の例をあげる。

1.  **GEC の生成**

生成の段階で実行コンテキストスタックに積み重なる。

```javascript
GEC {
	ThisBinding: window,
	LexicalEnvironment: {
		EnvironmentRecord: {
			b: <uninitialized>,
			func: func(){...}
		},
		outer pointer: null
	},
	VariableEnvironment: {
		EnvironmentRecord: {
			a: undefined,
			r: undefined
		},
		outer pointer: null
	}
}
```

2.  **GEC の実行**

```javascript
GEC {
	ThisBinding: window,
	LexicalEnvironment: {
		EnvironmentRecord: {
			b: 4,
			func: func(){...}
		},
		outer pointer: null
	},
	VariableEnvironment: {
		EnvironmentRecord: {
			a: 3,
			r: undefined
		},
		outer pointer: null
	}
}
```

GEC の後が FEC である。 `func()` を呼び出し、FEC を生成する。

3.  **FEC の生成**

```javascript
FEC {
	ThisBinding: window,
	LexicalEnvironment: {
		EnvironmentRecord: {
			arguments: { num: 4, length: 1 },
		},
		outer: GECの LexicalEnvironment
	},
	VariableEnvironment: {
		EnvironmentRecord: {
			t: undefined
		},
		outer: GECの LexicalEnvironment
	}
}
```

4.  **FEC の実行**

```Javascript
FEC {
	ThisBinding: window,
	LexicalEnvironment: {
		EnvironmentRecord: {
			arguments: { num: 4, length: 1 },
		},
		outer: GECの LexicalEnvironment
	},
	VariableEnvironment: {
		EnvironmentRecord: {
			t: 9
		},
		outer: GECの LexicalEnvironment
	}
}
```

FEC が実行され、スタックから削除されたら、GEC の `r` が 20 で初期化される。

```javascript
GEC {
	ThisBinding: window,
	LexicalEnvironment: {
		EnvironmentRecord: {
			b: 4,
			func: func(){...}
		},
		outer pointer: null
	},
	VariableEnvironment: {
		EnvironmentRecord: {
			a: 3,
			r: 20
		},
		outer pointer: null
	}
}
```

全 Code が実行されたため、GEC もスタックから削除されプログラムが終了する。

![GIF](https://miro.medium.com/max/1100/1*SBP65hdVDW5j0LuVryTiXw.gif)

<br>

## Reference

-   [What is the 'Execution Context' in JavaScript exactly?](https://stackoverflow.com/questions/9384758/what-is-the-execution-context-in-javascript-exactly)
-   [The ECMAScript “Executable Code and Execution Contexts” chapter explained](https://medium.com/@g.smellyshovel/the-ecmascript-executable-code-and-execution-contexts-chapter-explained-fa6e098e230f#f88f)
-   [ECMA-262-5 in detail. Chapter 3.2. Lexical environments: ECMAScript implementation.](http://dmitrysoshnikov.com/ecmascript/es5-chapter-3-2-lexical-environments-ecmascript-implementation/#this-binding)
-   [ECMAScript 5 spec: LexicalEnvironment versus VariableEnvironment](https://2ality.com/2011/04/ecmascript-5-spec-lexicalenvironment.html)
-   [Variable Environment vs lexical environment](https://stackoverflow.com/questions/23948198/variable-environment-vs-lexical-environment)
-   [ECMAScript 2020 Language Specification](https://tc39.es/ecma262/)
-   [JavaScript Internals: Execution Context](https://medium.com/better-programming/javascript-internals-execution-context-bdeee6986b3b)
