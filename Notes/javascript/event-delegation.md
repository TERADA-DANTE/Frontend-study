# イベント委任(Event delegation)

## Event bubbling と Capturing

Event Delegation の前に必ず Event bubbling と Capturing に関して理解しておくべきである。

**Event bubbling** とは, 下位 Element にて Event が発生した時、該当 Element を始め、上位 Element まで Event が移動(Propagation)することを示す。

**Event Capturing** とは、Event bubbling の逆。上位 Element で Event が発生し、下位 Element まで Event が移動(Propagation)することを示す。

✅ 移動を Propagation と説明した理由はこの移動を防ぐ Method が stopPropagation であるため。

下記のような例で説明を続ける。

HTML

```html
<div>
    <ul>
        <li>例題</li>
    </ul>
</div>
```

Javascript

```javascript
document
    .querySelector('li')
    .addEventListener('click', () => console.log('li クリック'))
document
    .querySelector('ul')
    .addEventListener('click', () => console.log('ul クリック'))
document
    .querySelector('div')
    .addEventListener('click', () => console.log('div クリック'))
```

上のように三つの Element に Event handler をつけ、 `li` をクリックすると下記のような結果が得られる。

Console

```
li クリック
ul クリック
div クリック
```

即ち、Event の基本的な動作は Bubbling である。この動作を Capturing にする場合は API option として `addEventListener()` の最後の引数に `{ capture: true }` 設定する。

下記のような例で説明を続ける。

Javascript

```javascript
document
    .querySelector('ul')
    .addEventListener('click', () => console.log('ul クリック'), {
        capture: true,
    })
```

上のように`ul`に Capturing option をつけてクリックすると下記のような結果が得られる。

Console

```
ul クリック
li クリック
div クリック
```

Capturing が発動し、`ul`から`li`に Event が移動するがまた Bubbling が動作し、`div` に Event が発生する。

<br>

## Event delegation

**Event delegation** (イベント委任)とは複数の下位 Element に一々 Event Handler をつけることなく、上位 Element に Event Handler をつけ下位 Element を Control することを示す。Event delegation は下記のような利点がある。

1. 動的に Element が追加されたとしても Handler を考える必要がない。
   2．Code の量が減る。
   3．Memory 上乗っている Handler が減るため Performance に利点がある。

下記に Event delegation の例がる。

HTML

```html
<ul onclick="alert(event.type + '!')">
    <li>1番目</li>
    <li>2番目</li>
    <li>3番目</li>
</ul>
```

`li` 三つに各々 Handler をつけることなく上位 Element の `ul` にだけ Handler を付けたことがわかる。

⚠ ただし、必ず Event delegation がいいわけではない。状況に合わせた判断を…

<br>

## Reference

-   [JavaScript Event Delegation is Easier than You Think](https://www.sitepoint.com/javascript-event-delegation-is-easier-than-you-think/)
-   [What is DOM Event delegation?](https://stackoverflow.com/questions/1687296/what-is-dom-event-delegation)
