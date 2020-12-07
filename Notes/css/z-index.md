# z-index の原理

## z-index と Stacking Context

z-index の前にまず Stacking Context の概念がある。 **Stacking Context とは, HTML 要素が User を基準にして仮想の Z 軸の上にある。3 次元の状態**であることを示す。
したがって Stacking Context を形成するとのことは 3 次元を形成することでその中の要素を z-index が決めるとのことである。

<img src="../../images/css/stacking context.png">

[Image from](https://tympanus.net/codrops/css_reference/z-index/)

上の画像のように、各要素が User が見る z 軸の上で z-index に合わせて**積み重なる**ことがわかる。これが Stacking Context で、これを形成する条件は[かなりおおい](https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context)
下記にいくつかの例がある。

-   **position が relative/absolute で z-index が auto ではない**
-   **position が fixed/sticky**
-   **opacity가 1 より低い**
-   **transform が none ではない**

Stacking Context は次のような特徴がある。

-   Stacking Context は **他の Stacking Context を含めることができる**。
-   Stacking Context で Stacking を考慮するのは **子要素のみ**。

即ち、2 個の Stacking Context がある場合、2 個は独立で、その中の子要素は親の中での Stacking Context だけを考慮する。

<br>

## 優先順位

Stacking Context を形成する要素が存在しない場合は次のようになる。

<img src="../../images/css/default stacking order.png">

[Image from](https://tympanus.net/codrops/css_reference/z-index/)

もし、等しい要素であれば Markup 順番で Stacking Context が決まる。

```html
<div>1</div>
<div>2</div>
<div>
    3
    <div>4</div>
    <div>5</div>
    <div>6</div>
</div>
```

総合敵に考えると Markup が上のような場合 `z-index` 下記のように積み重なる。

<img src="../../images/css/z-index stacking order.png">

[Image from](https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context)

-   div1 と div2, div3 は同じ Level にあるため、z-index より div2 > div3 > div1 順になる。
-   div4 と div5, div6은 div3 の中にあるため、**その中で** z-index より積み重なる。
    ⚠ div3 の中の要素の z-index は div1,div2 と関係がない。

<br>

## Reference

-   [CSSReference, z-index](https://tympanus.net/codrops/css_reference/z-index/)
-   [MDN, Stacking Context](https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context)
-   [MDN, z-index](https://developer.mozilla.org/ko/docs/Web/CSS/z-index)
