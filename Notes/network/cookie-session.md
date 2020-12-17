# Cookie vs Session

HTTP は Stateless な特徴を持っている Protocol である。つまり、User が Browser を通して Page に接続すると User の誰が接続したのかに関してはわからない。なので Cookie または Session を使い、User を区分する必要がある。

<br>

## Cookie

Cookie とは Client の Browser に保存される小さな Data である。これは Server が Client の Request を識別するのに使われる。Cookie を使うことで User を識別することは簡単になるが、Client が Cookie を修正することも、Cookie が奪われることも可能なため、Security 面では不利である。Id, Password などの情報を保存するには使われないが、次のような物を識別するに使われる。

- **Session ID**: Server に保存する大事な情報に対しての識別子、つまり、ID の ID
- **個人化** : User のテーマなど
- **Tracking** : User の行動分析

<br>

## Session

Session とは Browser が Server に接続されている間保存している Data である。User が Page に接続して Server に Request をすると、Server はその User を記憶し、識別する Session ID を`Set-Cookie` Header で Client に Response する。Client は Cookie で Session ID を管理し、Request するたびに `Cookie` Header に Session ID を含めて送信するため、Server は Client を識別することができる。次のような物を識別するに使われる。

- **大切な情報** : User ID, User Password

<br>

## 違い

- **Cookie**

  - Client 側に保存する。(Browser)
  - 指定した時間の間有効
  - 文字列のみ保存可
  - 速度が早い
  - Security の問題がある

- **Session**
  - Server に保存する。(Server の Memory,Database)
  - Browser を開いている間有効
  - 文字列+Object も保存可
  - 速度が遅い
  - Security の問題が少ない

<br>

## Reference

- [What are sessions? How do they work?](https://stackoverflow.com/questions/3804209/what-are-sessions-how-do-they-work)
- [CS 142: Web Applications (Fall 2010)](https://web.stanford.edu/~ouster/cgi-bin/cs142-fall10/index.php)
