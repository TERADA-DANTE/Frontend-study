# Reset.css vs Normalize.css

Chrome, Safari, IE など各 Browser は HTML 要素の基本的な Style を持っている。Reset.css、Normalize.css は CSS で Style を適用する時にこれが同一な適用を邪魔するため、Style を初期化方法である。

<br>

## Reset.css

**全 Browser の内蔵 Style を無くす方法**。無の状態から始まり、 `h1` ~ `h6` , `p` , `em` など各タグに適用されている Style をなくす。一番有名なのは [これ](https://github.com/shannonmoeller/reset-css)。初期化の後、各自の方式に合わせて使用することができる。

<br>

## Normalize.css

**全 Browser の内蔵 Style を統一させる方法**。 既存の Style を維持するが、Browser の違いをなくす方法. 一番有名なのが[これ](https://github.com/necolas/normalize.css/)。コメントから各要素を Styling する理由を表記している。

<br>

## 違いと選択

-   Reset.css の場合、全部初期化するため一から Style を適用していくことが難しい場合がある。Browser のバグに出会う恐れがある。
-   Normalize.css の場合、Browser の Update により、新しい内蔵スタイルが適用されると、新しい Version が必要となる。バグから比較的に自由な利点がある。

<br>

## Reference

-   [Stackoverflow, CSS reset - What exactly does it do?](https://stackoverflow.com/questions/11578819/css-reset-what-exactly-does-it-do)
-   [Stackoverflow, What is the difference between Normalize.css and Reset CSS?](https://stackoverflow.com/questions/6887336/what-is-the-difference-between-normalize-css-and-reset-css)
-   [About normalize.css](http://nicolasgallagher.com/about-normalize-css/)
