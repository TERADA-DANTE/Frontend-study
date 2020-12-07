# HTTP

Client-Server model に従う Protocol であり、TCP/IP 上で動作し、80 番 Port を使用して通信する。標準は HTTP/1.1 => HTTP/2 => HTTP/3 順で登場してきた。この文章は HTTP/1.1 に関してである。

## 特徴

### Connectionless

Client が Server から Resource を要請して Response をもらうと連結(Connection)を切ることが特徴である。連結を維持することは Server に負担をかけるおそれがあるため、数多い Client から Request をうける Server の場合 Response の後連結を切る。これによって Server の負担が減る利点はあるが、Resource を Request するたびに連結をするため Overhead 問題が発生する。これを解決するために Request header に`Connection: keep-alive`を追記し、Persistent connection を維持することができる。HTTP 1.1 からは Persistent connection が Default である。

### Stateless

Request が独立なことだと見なすことで、Server は Client の State を考慮しない。つまり、各 Client にあわせた Resource の Response は不可である。これを解決するために、Cookie、Session または Token 形式の Oauth、JWT などが使われる。

<br>

## Method

Client がサーバーに Request する方法を定義するもので Resource に対しての行動を要求する。

-   **GET** : Server に照会する Resource を要請する。 (READ、照会)
-   **POST** : Server に <u>生成する Data を body にいれ</u>送る. (CREATE, 生成)
-   **PUT** : Server に <u>修正する Data を body にいれ</u>送る. (UPDATE, 修正)
-   **DELETE** : Server に 削除する Resource を要請する。(DELETE, 削除)
-   **PATCH** : PUT と似たようなもので一部分だけ修正する。

<br>

## Response Code

Server は Client から Request をうけると Response 状態に合わせて下記のような Response Code を Client に返す。

-   **1xx (Request に関しての情報)** : Request をうけたら作業をし続ける。
-   **2xx (成功)** : Request を成功的に果たした。
    -   200(成功), 201(新しい Resource 作成), 202(Request 受付、処理待ち)
-   **3xx (Redirection)** : Client は Request を終わらすため、追加の動作をしなければならない。
    -   300(複数の Response からの選択), 301(永久移動, Request した Page が移動した場合), 302(臨時移動, 臨時的に Page が移動した場合)
-   **4xx (Client 問題)** : Client に問題がある。
    -   401(権限なし), 403(禁止, Resource に権限なし), 404(見つからない、Server に存在しない)
-   **5xx (Server 問題)** : Server に問題がある。
    -   500(内部 Server 問題), 501(該当機能無し, Method 認識不可), 503(サービス使用不可)

<br>

## Header

Request/Response header, body header など色んな属性がある。重要ないくつかを下記にて説明する。

### Request header

-   Host : Server domain name と TCP port number

    -   ```
        Host: en.wikipedia.org:8080
        ```

-   Content-Type : POST/PUT Method を使う時の body の type

    -   ```
        Content-Type: application/x-www-form-urlencoded
        ```

-   If-Modified-Since : 表記した日以来変更された Resource を獲得する。

    -   ```
        If-Modified-Since: Sat, 29 Oct 1994 19:43:31 GMT
        ```

-   Origin : Request の Domain origin を表記。Server の `Access-Control-*` に関係する。

    -   ```
        Origin: http://www.example-social-network.com
        ```

-   Cookie : Server の `Set-Cookie` で設定された Cookie 値

    -   ```
        Cookie: $Version=1; Skin=new;
        ```

### Response hader

-   Access-Control-\* : CORS を許可する Website を表記

    -   ```
        Access-Control-Allow-Origin: *
        ```

-   Set-Cookie : Client に Cookie 設定

    -   ```
        Set-Cookie: UserID=JohnDoe; Max-Age=3600; Version=1
        ```

-   Last-Modified : Request された最後に変更された時刻

    -   ```
        Last-Modified: Tue, 15 Nov 1994 12:45:26 GMT
        ```

-   Location : 3xx の場合 Redirect する Location

    -   ```
        Location: http://www.w3.org/pub/WWW/People.html
        ```

-   Allow : Request された Resource に対して可能な Method

    -   ```
        Allow: GET, HEAD
        ```

<br>

## Reference

-   [Wikipedia, List of HTTP header fields](https://en.wikipedia.org/wiki/List_of_HTTP_header_fields)
