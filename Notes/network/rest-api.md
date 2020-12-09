# REST API

Rest API とは REpresentational State Transfer の略で全般的な Web App にてコミュニケーションの時使用される Web architecture model である。つまり、Resource を送りあう**Web 上の通信で一般的なスタイルを規定した architecture**である。

## API とは

Application Programming Interface の略で Google API, Twitter API など **Application から Resource、機能をを借りて使う時使用する Interface のこと**。つまり、REST API は Rest の原則を基盤に Service を設計した API であり、大体の Host は REST API を提供する。

<br>

## REST の特徴

### Uniform Interface

REST が HTTP の標準を従う前提でどんな技術でも適用可能となる。つまり、Platform、言語の Limit がない。REST API の Response として Json が使われるが昔は XML も使っていた。

### Stateless

Server は Client の状況を考慮せず、API の Request に対して処理している。これを State がないと表現する。Client を考慮してないため実装が簡単になる。

### Cacheable

REST は HTTP を基盤に作られたため、HTTP の特徴である Caching を使うことができる。REST API を活用し、`GET`Method に`Last-Modified`を含めると Content の変化がない場合は Caching された情報が使われる。これにより Network response がなくなり、API request が発生しないため、Server の負担もなくなる。

### Client-Server Architecture

REST Server が API を提供し、Client はそれが提供する Docs により、行動する。Server と Client が依存関係がなくなり、独立性が高まる。

### Layered System

Client は Layered System が不可能であるが、Rest server の場合 Security、暗号化などを追加することができるし、Proxy、Gateway など中間媒体を使うことができる。

<br>

## REST API の特徴

### URI は Resource を表現する。

-   **Resource 名は名詞**

```
/students/1
```

-   **Resource は Collection と Document で表現する**

Collection は複数の表現

```
/locations/seoul/schools/3
```

`locations` は Collection、 `seoul` は Document となる。

<br>

### Resource に対しての行為は HTTP の Method で表現する。

-   **GET は Resource の照会**

```
GET /students
```

-   **POST は Resource の生成**

```
POST /students
```

-   **PUT は Resource の Update**

```
PUT /students/1
```

-   **DELETE は Resource の削除**

```
DELETE /students/1
```

<br>

## HTTP Status

Request に対する Response の Status を明確に返すのも REST API の設計の時大事である。

-   **2xx** : 成功 (200 Ok, 201 Created)
-   **3xx** : Redirection (304 Not Modified)
-   **4xx** : Client Error (400 Bad Request, 401 Unauthorized)
-   **5xx** : Server error (500 Internal Server Error)

<br>

마지막으로 아래 그림을 보고 정리해보자.

<img src="../../images/network/REST.png">

<br>

## 참고

-   [REST API concepts and examples(유튜브)](https://www.youtube.com/watch?v=7YcW25PHnAA)
-   [REST API가 뭔가요?(유튜브)](https://www.youtube.com/watch?v=iOueE9AXDQQ)
-   [REST API 제대로 알고 사용하기](https://meetup.toast.com/posts/92)
-   [REST API의 이해와 설계-#1 개념 소개](https://bcho.tistory.com/953)
-   [REST 아키텍처를 훌륭하게 적용하기 위한 몇 가지 디자인 팁](https://spoqa.github.io/2012/02/27/rest-introduction.html)
-   [Why Should We Choose REST (Client-Server) Model to Develop Web Apps ?](https://medium.com/@audira98/why-should-we-choose-rest-client-server-model-to-develop-web-apps-c3bb2451b13a)
