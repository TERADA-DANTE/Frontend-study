# img の下の空白

## img の下の空白

`<img>` タグは基本的に下に空白を生成する。

```html
<div class="container">
    <img
        src="https://images.unsplash.com/photo-1584380497382-2722e59ff33f?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=687&q=80"
        alt=""
    />
</div>
```

```css
.container {
    width: 300px;
    border: 1px solid crimson;
}

img {
    max-width: 100%;
}
```

<p align="center">
	<img src="../../images/css/img-space.png">
</p>

<br>

## 空白ができる理由

`<img>` タグは Inline-level 要素であり、一般テキストのように baseline 基準に整列される。これは`vertical-align: baseline`が Default とのことである。

<p align="center">
	<img src="../../images/css/img-baseline.gif">
</p>

[Image from](https://stackoverflow.com/a/34952703/11789111)

上の画像からテキストが Baseline を基準に整列されたことがわかる。`<img>`もそのようになっているため、y, j, p, g, q のような descender 文字のためにしたに空間ができる。

<br>

## 解決

⚠ `<img>` に `display: block` : Block-level 要素に変える。一行を全部占めることになる。

⚠ 親要素に `line-height: 0` : 子要素の `line-height`をなくす方法で、テキストにも影響があるため、いい方法ではない。

✅ **`<img>` に `vertical-align: middle/top/bottom`** : `vertical-align` を変える方法で、根本的な解決だといえる。

<br>

## Reference

-   [Image inside div has extra space below the image](https://stackoverflow.com/questions/5804256/image-inside-div-has-extra-space-below-the-image)
