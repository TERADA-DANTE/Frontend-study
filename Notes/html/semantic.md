# Semantic markup

Semantic とは"意味論的な"の意味で Markup とは HTML タグで文書を作成することを示す。したがって Semantic markup とは**意味を正確に伝えるように HTML 文書を作成すること**を示す。

## 作成方法

Semantic markup で最も大切なのはタグを用途に合わせて使うことである。

-   header/footer に `<header>` と `<footer>`
-   Main content に `<main>` と `<section>`
-   独立 Content に `<article>`
-   最上位題名に`<h1>`
-   順番のない目次に `<ul>` 、`<li>`
-   navigation に `<nav>`

上のようにタグが持っている意味に合わせて使用することで、以外にも CSS を明確に表記するタグを使わないのも Semantic markup の一部分である。**即ち、タグ自体が Style である場合これは Markup 自体が Style をもつことなので Semantic markup に相応しくない**

例として`<strong>` と `<b>` タグがある。どっちも Text を Bold 化するが、 `<b>`はただ Bold の略字である。これはタグ自体が Style を持ってると思えるが、`<strong>`の場合"中の内容が他の内容より強調されるべきである"との意味を持つため Semantic markup だと言える。

<br>

## 特徴

-   Search engine が Semantic markup を重要視するため、**SEO に有利**。
-   **Web アクセシビリティ** の向上.
-   `div` , `span` だけの要素より可読性が高い

Semantic markup は理想論に近い技術で Web site 設計の時に深く考慮するのが望ましい

<br>

## Reference

-   [Stackoverflow, What are the benefits of using semantic HTML?](https://stackoverflow.com/questions/1729447/what-are-the-benefits-of-using-semantic-html)
-   [Stackoverflow, What's the difference between and , and ?](https://stackoverflow.com/questions/271743/whats-the-difference-between-b-and-strong-i-and-em)
-   [MDN, Semantics](https://developer.mozilla.org/ko/docs/Glossary/Semantics)
