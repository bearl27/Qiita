---
title: 【基本情報・応用情報】ロールバックとロールフォワードの違いについて
tags:
  - error
  - トランザクション
  - DBMS
  - 基本情報技術者試験
  - 応用情報技術者
private: false
updated_at: '2024-10-21T12:42:01+09:00'
id: 48ea517e5debbff3b2e9
organization_url_name: rits-rcc
slide: false
ignorePublish: false
---
# ロールバック（後退復帰）
システム障害が発生した時に，システムを以前の**安定した**状態に戻すこと．
「最新のチェックポイント後のことはどうでもいいからとりあえず安定した場所まで戻したい！！」というときに使う．

> git reset --hardと考えるとわかりやすいかも

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3748983/c47f8ad8-dae1-fa70-5e2e-3a3dc223906b.png)


# ロールフォワード（前進復帰）
システム障害が発生した時に，一度チェックポイント時点の状態まで戻し，ログに記録された変更を適用して状態を進めることによりシステム障害が起きる直前の状態に復元すること．
「最新のチェックポイント後にかなり進んだから，できるだけ多くの変更を保持しつつ復旧したい！！」というときに使う．
障害発生時に単に前の状態に戻るだけでなく、問題の原因を特定し修正した上で、有効な変更を再適用するという含む．

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3748983/879a6bcd-77b4-2e57-041d-7a3510d23e95.png)


# 問題
1~5について，システム障害が発生したときにロールフォワードをによって障害回復できるトランザクションを選べ．

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3748983/dc761c0e-9e4b-fdcd-e8e2-612df46e1eb5.png)

|
|
|
|
|
|
|
|
|
|

## 答え
1と4
## 解説
**1・4** : 
チェックポイント後にコミットしているため，チェックポイントの状態に戻してからロールフォワードによって更新直後の状態に戻せる．
**2・3** : 
チェックポイント後にトランザクション処理中に障害が発生したのでロールフォワードはできない...そのため，ロールバックによって更新前の状態に戻す．
**5** : 
チェックポイント前にコミットされているため，ロールバックもロールフォワードも不要である．

# 最後に
10/13に応用技術者試験がありますね！
受ける人は共に頑張りましょう！！！
それではみなさんよいエンジニアライフを〜👋

# 基本情報・応用情報記事

https://qiita.com/bearl27/items/48ea517e5debbff3b2e9

https://qiita.com/bearl27/items/c08be5f2a53fd3fb7b53

https://qiita.com/bearl27/items/e63a6fb14eba0067d940

https://qiita.com/bearl27/items/f8cf339e7f966291683d

https://qiita.com/bearl27/items/849c9400ae93608331e7
