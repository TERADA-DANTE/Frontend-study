# Javascript engine が Code を実行する過程

Javascript を実行するためには Javascript engine が必要となる。そして Browser は Javascript engine を内蔵している。Engine の種類は Browser によって異なるが、Javascript の Code を実行する方法はさほど変わらない。その種類には V8, SpiderMonkey, Javascript core などがある。

<img src="../../images/javascript/engine-overview.png">

[image From](https://mathiasbynens.be/notes/shapes-ics)

下記にて上記の画像を説明する。

1. Engine は Code に出会うと Parsing する。そして Code は**AST(Abstract Syntax Tree)** と変換される。
2. **Interpreter** は AST を基盤にして **Bytecode を生成** する.
3. Interpreter が Bytecode を実行する前に、 よく使われる関数、Type 情報などがある Profiling data と共に Bytecode を Optimizing compiler に送る（Optimizing を和訳すると最適化）
4. Optimizing compiler は Profiling data を基盤にして **Optimized code を生成** する。
   ⚠ Profiling data の中に **間違えたところがあると最適化を解除し、Deoptimize** また Bytecode を実行しようとする過程を繰り返す。

<br>

## Reference

-   [JavaScript engine fundamentals: Shapes and Inline Caches](https://mathiasbynens.be/notes/shapes-ics)
