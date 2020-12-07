# Block Formatting Context

MDN によると、

> ブロック整形コンテキスト(block formatting context)は、ウェブページにおける CSS の視覚的なレンダリングの一部です。ブロックボックスのレイアウトが行われ、浮動が他の要素と相互作用する領域です

Block Formatting Context は[margin-collapsing](https://github.com/TERADA-DANTE/Frontend-study/blob/main/Notes/css/margin-collapsing.md)の対策の優れた対策でもある。

<br>

## 生成条件

BFC は以下のいずれを満足するものである。

-   root もしくはこれを含めてる要素
-   `float`が none でないながら clear してない場合
-   `position`が absolute / fixed
-   `display`が inline-block / tabel-cell / tabel-caption
-   `overflow`が visible でない
-   `display`が flex / inline-flex

つまり、以下の 5 つは全部 BFC を生成する。

HTML

```html
<div class="float"></div>
<div class="position"></div>
<div class="display"></div>
<div class="overflow"></div>
<div class="flex"></div>
```

CSS

```css
.float {
    float: left;
}
.position {
    position: absolute;
}
.display {
    display: inline-block;
}
.overflow {
    overflow: hidden;
}
.flex {
    display: flex;
}
```

<br>

## 活用

1. **margin-collapsing の対策**

HTML

```html
<div class="bfc">
    <p>element</p>
    <p>element</p>
    <div class="new-bfc">
        <p>element</p>
    </div>
</div>
```

CSS

```css
div {
    background-color: blue;
}
p {
    margin: 10px 0;
    background-color: green;
}
.bfc {
    overflow: hidden;
}
.new-bfc {
    overflow: hidden;
}
```

本来なら`p` の間は 10px の margin-collapsing で 20px ではなく 10px の margin を持つ。この場合新しい BFC を生成し、`p`を入れることで margin-collapsing を解決できる。

2. **float の要素を含める**

```html
<div class="container">
    <div class="float"></div>
</div>
```

```css
.container {
    border: 3px solid red;
    overflow: hidden;
}

.float {
    float: left;
    width: 500px;
    height: 300px;
    background-color: yellow;
}
```

普通 float の要素を含めるために `.clearfix`を使うが新しい BFC を作ることで解決できる。

3. **float の要素を囲む Text を分離**

```html
<div class="container">
    <div class="box"></div>
    <p>多い量のText....</p>
</div>
```

```css
.container {
    border: 3px solid red;
    overflow: hidden;
}
.box {
    float: left;
    width: 100px;
    height: 100px;
    background-color: green;
}

p {
    overflow: hidden;
}
```

`p` タグで新しい BFC を作り、float 要素を庇わないようにできる。

<br>

## Reference

-   [Understanding Block Formatting Contexts in CSS](https://www.sitepoint.com/understanding-block-formatting-contexts-in-css/)
-   [MDN, Block formatting context](https://developer.mozilla.org/ko/docs/Web/Guide/CSS/Block_formatting_context)
