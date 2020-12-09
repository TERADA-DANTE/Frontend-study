# new の原理

new 演算子を使用すると、開発者はユーザー定義のオブジェクト型やコンストラクタ関数を持つ組み込みオブジェクト型のインスタンスを作成することができる。

つまり、

1. 空白のプレーンな JavaScript オブジェクトを作成します。
2. 他のオブジェクトを親プロトタイプとすることで、新しく作成されたオブジェクトと他のオブジェクトをリンク（コンストラクターを設定）します。
3. ステップ 1 で新しく作成されたオブジェクトを this コンテキストとして渡します。
4. 関数がオブジェクトを返さない場合は this を返します。

```javascript
function Func() {}
const f = new Func()
```

-   空白 Object `{}`が作成される。
-   該当 Object の `[[Prototype]]` は `Func.prototype` 。
-   この Object を `this` にする。
-   `Func()` を呼び出し、 `this` コンテキストとして渡す。
-   関数が Object を返さないので (`undefined` ) this を返す。

<br>

## Reference

-   [Stackoverflow, What is the 'new' keyword in JavaScript?](https://stackoverflow.com/questions/1646698/what-is-the-new-keyword-in-javascript)
-   [Stackoverflow, How does the new operator work in JavaScript?](https://stackoverflow.com/questions/6750880/how-does-the-new-operator-work-in-javascript)
