# data- 属性

data- 属性とは**DOM に Data を保存できる User 定義 Data 属性**であり、`data-`の次の値が Data となる。data- 属性は使用しようとする用途に適切な属性や要素がない時使われ、該当 Page が **独自で使う値** であ。なので Page と独立な Software がこの属性を使ってはいけない。

例として音楽サイトで曲を長い順で整列する時に`data-` 属性で音楽の再生時間を入力したとする。

HTML

```html
<ol>
    <li data-length="2m11s">壊れかけのRadio</li>
    ...
</ol>
```

もし、この Page と関係のない外部から音楽時間を調べるために使用するとなるとこれは`data-` 属性に相応しくないことである。つまり、`data-` 属性は該当サイトのみの Data、該当サイトの Script のための属性である。

<br>

## Reference

-   [W3, Custom Data Attribute](https://www.w3.org/TR/2011/WD-html5-20110525/elements.html#custom-data-attribute)
