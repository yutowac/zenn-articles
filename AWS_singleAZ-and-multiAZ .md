## AWSのデータベース選定時の設計にある「シングルAZ」「マルチAZ」とは？

私の場合はAWS pricing calculatorを使ってクラウドアーキテクチャー全体の費用を算出しようとした時に発見してふと疑問に思いました。
AWSのマネジメントコンソールからデータベースのデプロイオプションを選ぶときにも必要だと思います。

<img width="786" alt="スクリーンショット 2024-06-28 222043" src="https://github.com/yutowac/Zenn-Articles/assets/44987057/2184beb7-3635-4b85-89df-9fe0fb08a2cb">

[AWS pricing calculator](https://calculator.aws/#/)

## AZとは？
AZはAvailability Zoneの略称で、複数の「データセンター（DC）」から構成されるインフラ設備の単位です。
例えば東京リージョンには次のようなAZがあります。
- ap-northeast-1a
- ap-northeast-1b
- ap-northeast-1c
- ap-northeast-1d
 
AZ同士は独立しているため、障害が出た際にシステムを停止させずに稼働させることができます。

## シングルとマルチの違い
名前の通り、シングルAZは1つだけAZを使いマルチAZは複数のAZを使う仕組みです。
前述したとおり、マルチAZにすることで稼働中のAZが停止した時にシステム全体を止めることなく、システムを稼働し続けることができます。
ただしAZの台数が増えるのでその分費用がかかります。

![image](https://github.com/yutowac/Zenn-Articles/assets/44987057/e9571143-f6d6-4d90-b9f5-b489f0ef5a0d)

[マルチAZの仕組み](https://aws.amazon.com/jp/rds/features/multi-az/)
