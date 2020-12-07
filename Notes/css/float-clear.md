# float を解除する方法

`float` Property を子 Element に適用すると親 Element が子 Element の`height`を感知することができない。なのでこれを克服する方法を知っておくべきである。
下記の例で説明を続ける。

⚠ `float`を解除するとの意味は`float`の Property を削除するのではなく、`float`の影響から自由にすることを示す。
HTML

```html
<div class="parent">
    おや
    <div class="child">こども</div>
</div>
```

CSS

```css
.child {
    float: left;
}
```

<br>

## 親 Element にも `float` を適用

-   子 Element を含むサイズになる。
-   親 Element の親 Element にもずっと`float` を適用が必要となる。

```css
.parent {
    float: left;
}
```

<br>

## 親 Element に`overflow` Property 適用

-   `overflow: auto`
    子 Element が比較的に大きいと Scroll が生じる。

-   `overflow: hidden`
    子 Element が比較的に大きいと切られる。

```css
.parent {
    overflow: hidden;
}
```

<br>

## 親 Element の最後に Empty Element を作成し、`clear` Property を適用

❌ 意味ない Element となるためおすすめできない。

```html
<div class="parent">
    ...
    <div class="clearfix"></div>
</div>
```

```css
.clearfix {
    clear: both;
    height: 0;
    overflow: hidden;
}
```

<br>

## 親 Element に `display: inline-block` Property 適用

-   若干の余白が生じる。
-   親 Element に `float` を適用したのと似たような結果。

```css
.parent {
    display: inline-block;
}
```

<br>

## pseudo-Element として `clear` Property 適用

✅ おすすめ

```css
.parent::after {
    content: '';
    display: block;
    clear: both;
}
```

<br>
