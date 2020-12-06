# Same Origin Policy

Same Origin Policy とはある文書または Script が他の **Protocol、Port、Host** にある Resource を使用することを制限する Policy。

下記にてその例を述べる。

```
http://website.com/ex/ex.html
```

|         Resource request         |         成功         |
| :------------------------------: | :------------------: |
|      http://website.com/ex/      |          ✅          |
|     http://website.com/ex1/      |          ✅          |
| http://website.com:81/ex/ex.html |   ❌ Port の違い   |
|     http://wwebsite.com/ex/      |   ❌ Host の違い   |
|  https://website.com/ex/ex.html  | ❌ Protocol の違い |

上のように Host、Port、Protocol、いずれ一つも違う場合 Same Origin Policy の対象となり Request に失敗する。

<br>

## 解決方法

### `document.domain`

臨機応変な方法として Domain の設定を変えることで SOP を避けることができる。現在 Domain が`http://store.company.com/index.html` だとすると、

```javascript
document.domain = 'company.com'
```

上のようにして `http://company.com/index.html` に Request を送ることができる。ただし、該当 Script が複数の HTML に関連する場合は全部上のように設定すること、Firefox は支援してないこと、そしてこれは Server―Client の通信ではなく、**Client 上で Origin が違う Frame に対して使用される方法である。**
したがって、Server とはこの方法で通信することはできない。

### CORS(Cross-Origin Resource Sharing)

HTTP Header を使って Client、Server にお互いの存在を認知させ、他の Origin の Resource を使うことを許可する方法。Client が Server に HTTP Request する時、HTTP Header の `Origin` Property に自動的に値が与えられる。

```
Origin: http://company.com
```

上の Domain から他の Origin の Resource を使うために AJAX Request をすると SOP により失敗する。 これを解決するために Server の HTTP Response Header に下記のように Request を許可する Domain を作成する。

```
Access-Control-Allow-Origin: http://company.com
```

### Proxy Server

Proxy Server は Client と Server の間で Data の交換を手伝う Server である。Server 側の`Access-Control-Allow-Origin`Property を修正できない時に有効な方法である。Proxy Server が Server に Request し、Response を保管したのを Client がもらう方法である。

Apache や Nginx のような Server で Proxy Server 機能を活性化することができるし、CRA(Create-React-App)の場合 `package.json` の `proxy ` 値を使い Proxy Server 機能を使うことができる。ただし、これはもう一個の Server を置くことになるため、Request の速度が落ちる短所がある。

<br>

## Reference

-   [Velog, CORS: Real examples](https://velog.io/@leejh3224/CORS-Real-examples-8yjnloovl5)
-   [Stackoverflow, Ways to circumvent the same-origin policy](https://stackoverflow.com/questions/3076414/ways-to-circumvent-the-same-origin-policy)
-   [Stackoverflow, Why doesn't setting document.domain work to allow AJAX requests to a parent domain?](https://stackoverflow.com/questions/15563611/why-doesnt-setting-document-domain-work-to-allow-ajax-requests-to-a-parent-doma)
-   [Stackoverflow, What is JSONP, and why was it created?](https://stackoverflow.com/questions/2067472/what-is-jsonp-and-why-was-it-created)
