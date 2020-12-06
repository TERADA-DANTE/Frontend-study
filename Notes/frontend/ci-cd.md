# CI と CD

## CI (Continuous Integration, 持続的な統合)

CI は Build と Test を自動化し、共有 Storage に併合させる Process を意味する。Git などの Version 管理ツールを使用する時複数の開発者が一つの共有 Storage を使うことが多い。この場合新しいコードの変更事項が Storage に統合されないことがある。したがって Build/Test の自動化から Code の一貫性(Consistency)を提供するため、持続的な統合という用語を使っている。

<br>

## CD (Continuous Delivery/Deploy, 持続的な伝達、配布)

CD は CI の Build/Test を通して正常的に確認すると配布を仕方によって 2 種類に分かれる。

-   **持続的な伝達** : Production 配布のための状態になり、配布自体は手動で行う。
    -   開発チームとビジネスチームのコミュニケーション不足問題を解決できる。
-   **持続的な配布** : Production まで自動で配布する。
    -   アプリケーションの提供速度が増加する。

<br>

CI/CD の 代表的なサービスとしては Jenkins, Travis CI, Circle CI などがあり、下記のように表現できる。

<img src="../../images/frontend/ci-cd.png">

[Image from](https://aws.amazon.com/ko/devops/continuous-integration/)

<br>
