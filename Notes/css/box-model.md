# Box Model

<p align="center">
	<img src="../../images/css/box model.png">  
</p>

Box Model とは**HTML 上の要素は視覚的な目的として全ての要素を四角いボックス**として考えることである。Box はしたのような Area をもっている。

-   **Content Area** : コンテンツ、Text や Image、Video など要素の実際の内容を含めている。
-   **Padding Area** : 内側の枠(Padding Edge)が囲んでいる Area。 Content Area の外から要素の内側の余白までを示す。
-   **Border Area** : 枠の線(Border Edge)が囲んでいる Area。Padding Area の外から Border Edge までを示す。
-   **Margin Area** : 外側の線(Margin Edge)が囲んでいる Area。枠を超え、隣接する要素まで拡張される。

<br>

## box-sizing

`box-sizing` Property を使い、 `width` と `height` が Content Area 基準か、Border Area 基準かを決めることができる。

-   `box-sizing: content-box` : Default。Content Area 基準。
-   `box-sizing: border-box` : Border Area 基準。

<br>

## Reference

-   [W3, CSS Box Model Module Level 3](https://www.w3.org/TR/css-box-3/)
-   [BrainJar, CSS Positioning](http://www.brainjar.com/css/positioning/)
