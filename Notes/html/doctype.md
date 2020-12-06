# DOCTYPE

DOCTYPE は Document Type の略で、**HTML がどの Version で作成されたか予め宣言し、Browser が内容を正確に表示するように指示するもの**である。`<!DOCTYPE>`で宣言するが、これを宣言しないと Browser は**quirks mode** で動作する。quirks mode(互換モード)の場合 Browser ごとに文書を表す方式がかなり異なるため、Cross Browser Issue の問題が発生する。

## DTD(Document Type Definition)

DTD(Document Type Definition)は文書形式を定義したもので DOCTYPE を表示する時に使われる。即ち、HTML 文書がどのような形式を従うのか DOCTYPE にて DTD を指定するものである。

DTD の例としては以下のようなものがあり、[W3C Recommended list of Doctype declarations](https://www.w3.org/QA/2002/04/valid-dtd-list.html) にてその詳細を確認することができる。

-   XHTML 1.1
-   XHTML 1.0
    -   Strict DTD
    -   Transitional DTD
    -   Frameset DTD
-   HTML 4.01
    -   Strict DTD
    -   Transitional DTD
    -   Frameset DTD
-   HTML 5

現時点では HTML5 の DTD の DOCTYPE が一番望ましいと思われる。

```html
<!DOCTYPE html>
```

<br>

## 참고

-   [What is DOCTYPE?](https://stackoverflow.com/questions/414891/what-is-doctype)
-   [What is difference between XHTML and HTML?](https://stackoverflow.com/questions/4153403/what-is-difference-between-xhtml-and-html)
