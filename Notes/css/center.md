# 横/縦真ん中に整列

## div の場合

```html
<div class="position-margin"></div>
<div class="position-transform"></div>
<div class="flex">
    <div></div>
</div>
```

上のような HTML の場合次のような方法が考えられる。

### position と margin

```css
.position-margin {
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    margin: auto;
}
```

本来`div`は親要素の`width`を従うため、自身の`width`があったとしても見えない部分がある。この特徴を利用し、`margin: 0 auto`で横基準真ん中に整列することができる。
また`position: absolute`を使い`left` , `right` , `top` , `bottom`を全部 0 にすることで見えない部分が画面全体を占める。ここで`margin: auto`が外側の余白を作るため、全体的に真ん中に整列することができる。

### position と transform

```css
.position-transform {
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
}
```

`div` を親基準上から、左から 50%離した後、自分の`width`, `height`の 50％を逆方向に戻す。

⚠ left, top の基準が左上であるため、逆方向に戻す必要がある。

### flex

```css
.flex {
    display: flex;
    justify-content: center;
    align-items: center;
}
```

親要素に`display: flex`を与え、子要素を整列する方法。支援してない Browser があるが、有用に使える。

<br>

## Text の場合

### padding

```html
<div>
    <span>テキスト</span>
</div>
```

```css
div {
    text-align: center;
    padding: 3em 0;
}
```

親要素に `text-align: center` を設定し、子要素のテキストを横基準真ん中に整列した。あと、`padding`を上下に設定し縦基準真ん中に整列した。ここで使われる`em`単位は Element の Font のサイズの 3 倍を意味する。即ち、Font のサイズが変わると`padding`も変わるため動的に縦の真ん中整列ができる。

### line-height

```css
div {
    height: 100px;
}
span {
    line-height: 100px;
}
```

テキスト縦サイズをを親の`height`と等しくする。

### Image の場合

```html
<div>
    <img src="イメージのアドレス" />
    <span>テキスト</span>
</div>
```

```css
img {
    vertical-align: middle;
}
```

イメージの整列も似たようなものであるが、Font の Baseline を基準に配置されるため、Font を Middle にあわせないと正確に真ん中に整列することができない。
<br>

## Reference

-   [Stackoverflow, Best way to center a on a page vertically and horizontally?](https://stackoverflow.com/questions/356809/best-way-to-center-a-div-on-a-page-vertically-and-horizontally)
