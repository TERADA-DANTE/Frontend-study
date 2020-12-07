# 標準モードと互換モード(Standard mode and quirks mode)

過去の Web Page は netscape と Explore の Version が別々存在し、標準がなかった。しかし W3C が Web 標準を作ってから Browser が既存の Web サイトを正確に表現できないことが生じた。その対策として Browser は Page を Rendering する時標準 モード(Standards mode)と 互換 モード(Quirks mode)で Rendering する Option を提供した。

**Browser は HTML が DOCTYPE をもっていないと 互換モードで, もっていると提供された DOCTYPE に合わせて 標準モードで Rendering する**。
互換モードで Rendering すると、古い Web page を最新の Browser でも歪みなく見ることができるが、互換モードの機能は Browser によって様々であり、Bug の可能性がある。例として、IE の場合互換モードでは[Box model](https://github.com/TERADA-DANTE/Frontend-study/blob/main/Notes/css/box-model.md)の解釈に Bug がある。

結論的には特別でない限り、DOCTYPE を表記し、Browser が標準モードで Rendering するようにする。現時点では HTML5 がおすすめしている。`<!DOCTYPE html>` を表記するのが一番望ましい。

<br>

## Reference

-   [What is quirks mode?](https://stackoverflow.com/questions/1695787/what-is-quirks-mode)
