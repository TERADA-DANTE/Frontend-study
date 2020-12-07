# script, script async, script defer

-   `<script>` : HTML Parsing が中断され、即座 Script が Loading され、その後 Parsing が再開される。
-   `<script async>` : HTML Parsing と並列的に Loading される。Script が実行される時は Parsing が中断される。 Google analytics など他の Script が依存しない独自的な Script を Loading する時適切である。

**async と defer の場合 `src` 属性は必須**

<img src="../../images/html/script.png">

<br>

## Reference

-   [Script Tag - async & defer](https://stackoverflow.com/questions/10808109/script-tag-async-defer)
