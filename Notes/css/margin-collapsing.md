# margin が重なる場合

margin が重なる場合を Margin-Collpasing という。Margin-Collpasing とは Block-level element の場合発生し、左右方向には適用されない、 **縦の方向のみ** 適用されることである。2 個の要素の margin が重なる場合はより大きい margin で庇う(overwrap)する方式で一個の margin が 0 より低い場合はタス方式である。

<br>

## 3 つの例

Margin-Collpasing は Block-level element の以下の 3 つの場合に発生する。

1. **隣接する Element**

```html
<div class="element1"></div>
<div class="element2"></div>
```

```css
div {
    width: 100px;
    height: 100px;
    background-color: red;
}
.element1 {
    margin-bottom: 20px;
}
.element2 {
    margin-top: 40px;
}
```

<p align="center">
<img src="../../images/css/margin-collapsing1.png">
</p>

element2 の`margin-top`がより大きいため、隣接する Element の感覚は 40px となる。

2. **親 Element と最初/最後の子 Element の間**

HTML

```html
<div class="parent">
    <div class="child"></div>
</div>
```

CSS

```css
div {
    width: 100px;
    height: 100px;
}
.parent {
    background-color: red;
    margin-top: 20px;
}
.child {
    background-color: blue;
    margin-top: 20px;
}
```

<p align="center">
<img src="../../images/css/margin-collapsing2.png">
</p>

2 個の margin が等しいため、20px となり、重なってしまう。**親 Element に inline content, border, padding** などで解決できる。

CSS

```css
.parent {
    background-color: red;
    border: 1px solid red;
    margin-top: 20px;
}
```

<p align="center">
<img src="../../images/css/margin-collapsing3.png">
</p>

3. **からの Element**

```html
<div class="empty"></div>
<div class="element"></div>
```

CSS

```css
.empty {
    margin-top: 50px;
}
.element {
    width: 100px;
    height: 100px;
    background-color: red;
    margin-top: 100px;
}
```

<p align="center">
<img src="../../images/css/margin-collapsing4.png">
</p>

高さのないからの Element がある場合も Margin-Collpasing が発生し、この場合 margin が 100px となる。**からの Element に height, min-height, padding, border**などの Property を提供し、堺を作ることで解決できる。

CSS

```css
.empty {
    border: 1px solid red;
    margin-top: 50px;
}
```

<p align="center">
<img src="../../images/css/margin-collapsing5.png">
</p>

<br>

## 例外

`position: absolute` , `float: left` , `display: flex` など Margin-Collpasing が発生しない場合がある。 **新しい BFC(Block Formatting Context)を生成することで Margin-Collpasing が解決できる** と考えておくべきである。
