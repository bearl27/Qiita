---
title: 自分でホワイトクリスマスにしちゃおうぜ【UnityでParticle Systemを使って雪を降らせる方法】
tags:
  - Unity
  - 3D
  - ゲーム制作
  - particle
  - クリスマス
private: false
updated_at: '2024-12-24T22:30:47+09:00'
id: dda008ad1ceb73dbd123
organization_url_name: rits-rcc
slide: false
ignorePublish: false
---
# はじめに
メリークリスマス🎄本日は2024年12月24日ということですが、わたしの所在地（大阪）では雪が降っていません。それは悲しいなということで、自分で雪を降らせました！！
本記事ではUnityのParticle Systemを使って雪を降らせる方法を学ぶ会です。ではやっていきましょう!

# 手順
1. [ParticleSystemを作る](#1-particlesystemを作る)
1. [位置と向きを調整する](#2-位置と向きを調整する)
1. [各パラメーターの設定](#3-各パラメーターの設定)
    3-1. [基本パラメーター](#3-1-基本パラメーター)
    3-2. [Emission](#3-2-emission)
    3-3. [Shape](#3-3-shape)
    3-4. [Color over Lifetime](#3-4-color-over-lifetime)
    3-5. [Size over Lifetime](#3-5-size-over-lifetime)
    3-6. [Noise](#3-6-noise)
1. [さいごに](#さいごに)

---

## 1. ParticleSystemを作る
Hierarchyタブで右クリックして以下図のように`Effects`→`Particle System`を作成する。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3748983/d3e5838c-caab-3afe-ba2b-06bcc29fd448.png)

## 2. 位置と向きを調整する
以下図のようにInspectorタブを開き、Transformを以下図のようにする。
デフォルトでは上向きにParticleが湧いている状態なので、降らすためにPositionを少し高い10にして、RotationXを90にします。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3748983/8236e48e-784c-ae85-b8a4-f794d27bf2ab.png)

## 3. 各パラメーターの設定
### 3-1. 基本パラメーター
今回使うパラメーターについて
| パラメーター | 説明 | 値 | 
|------------|------|--|
| Duration | パーティクルシステムの継続時間 | 10 | 
| Prewarm | システム開始時に1サイクル分を事前計算するか | ☑️ | 
| Start Lifetime | 個々のパーティクルの生存時間 | 5 |
| Start Speed | パーティクルの初期速度 | 3 |
| Start Size | パーティクルの初期サイズ | *1 |

*1 : 雪の大きさにはばらつきがあるので、ランダムに設定したい。Start Sizeの右の↓から`Random Bitween Two Constants`を選び、0.5~0.8にする。


![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3748983/1de5aaac-628f-894f-c55d-c0b36e5967a0.png)



![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3748983/2eea8eb1-e7ed-fd7f-5562-ba28ec8cbf3e.png)

### 3-2. Emission
Rate over Time : 1秒あたりの放出する数→20
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3748983/4e148a54-bc6c-1d22-e10b-a4e34712c140.png)

### 3-3. Shape
Shape: 放出元の形
Texture: 放出するものの形
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3748983/dd9cf5ec-9cdb-f30b-8070-d3d9d4b8b03b.png)



Scene Toolsは各種設定をGUIで操作できる。
| 説明 | ![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3748983/13022636-3c1a-8db1-91e5-6f25bdbe69c3.png) | ![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3748983/1fc50b8c-5cf7-54bd-7cba-48b39ddddf54.png) |
|:-:|:-:|:-:|
| 操作内容 | 位置や角度(Position・Transform)  |　放出する範囲(Scale)  |
| GUI |  ![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3748983/a87a223a-9525-d0f6-73a6-1a10f9751210.png) | ![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3748983/bc5a2070-0bfd-18a0-63d9-015141097e57.png)  |

### 3-4. Color over Lifetime
これは雪の寿命に対する色の変化を設定できます。
Colorの↓をクリックし、`Random Between Two Gradients`を選択します。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3748983/7d789434-1c2f-a060-75e4-15a42bb41181.png)
そして、Colorの2段目の白色をクリックすると`Gradient Ediotor`が開きます。
そして、以下図のように設定すると、寿命が70%の時から少しずつ透明になっていくようになります。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3748983/ad8afa77-5167-cf0b-24e3-e99437ac85e0.png)

:::note info
Gradient Editorで↓の増やし方はカラーパレットの少し上をクリックする
:::

### 3-5. Size over Lifetime
これは雪の寿命に対する大きさの変化を設定できます。
sizeの波をクリックすると波が赤くなり，inspectorタブの下の方に`Particle System Curves`ができる。そこで以下図のように設定する。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3748983/75c350c1-184c-3ab4-07e8-26b25fa51eb3.png)

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3748983/6eff91f2-e2e0-2b5c-907e-619cf4fb1856.png)

:::note info
新しい点を作るには波上をクリックする
下の概形をクリックするとテンプレートを選ぶことができ，それから変更していくと簡単に設定できる
:::

### 3-6. Noise
雪の振り方にノイズをかけます。ノイズをかけることで、雪がゆらゆらと落ちてくるように見せることができます。
`Strength`の右にある↓から`Random Bitween Two Constants`を選び、値を0.2~0.8にします。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3748983/c6e9b6a0-bb9f-0a55-9197-39935c9e9777.png)

---
***完成***
あとは自分好みに色々パラメーターをいじってください

---
# さいごに
今回はクリスマスイブということで、雪を降らせちゃいました！今年の私はキーたんと共にすごせたんでクリぼっちでありません‼️これからもよろしくね、キーたん❤️
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3748983/3e11a018-442a-fdae-60e6-3909b6c26455.png)
