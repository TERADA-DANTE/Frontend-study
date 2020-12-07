# local storage vs session storage vs cookie

local storage、session storage、cookie は全部 Client 上で Key/Value を保存するメカニズムであり、**value は必ず文字列**である。
また 全部 [SOP](https://github.com/TERADA-DANTE/Frontend-study/blob/main/Notes/security/sop.md)に従うため、他の Domain からの接近は禁じられている。

各特徴は下記のような形である。

|                 | cookie          | local storage | session storage            |
| --------------- | --------------- | ------------- | -------------------------- |
| 生成者          | Client/Server   | Client        | Client                     |
| 持続時間        | 設定による      | 消すまで      | タブ / Window を閉じるまで |
| 容量            | 5KB             | 5MB / 10MB    | 5MB                        |
| Server との関係 | O               | X             | X                          |
| 弱点            | XSS / CSRF 攻撃 | XSS 攻撃      | XSS 攻撃                   |

<br>

## Reference

-   [What is the difference between localStorage, sessionStorage, session and cookies?](https://stackoverflow.com/questions/19867599/what-is-the-difference-between-localstorage-sessionstorage-session-and-cookies)
-   [Local Storage vs Cookies](https://stackoverflow.com/questions/3220660/local-storage-vs-cookies)
