---
title: Flutter環境構築 Mac (CocoaPods編)
tags:
  - Mac
  - 環境構築
  - CocoaPods
  - Flutter
private: false
updated_at: '2024-04-12T18:00:25+09:00'
id: 8590bf22beebd3ec6f6c
organization_url_name: rits-rcc
slide: false
ignorePublish: false
---
自分の環境

Mac M2

CocoaPodsをダウンロードする際にとても手間がかかったため，同じような人がいたときに参考になればなあと思い書いてみました．

1. Rubyの更新
    
    `brew install ruby` 
    
    [Download RubyGems | RubyGems.org | your community gem host](https://rubygems.org/pages/download)
    
2. drdのインストール
    
    `gem list drb` でdrbのバージョンを確認.
    
    ```jsx
    gem list drb
    
    *** LOCAL GEMS ***
    ```
    
    と出力された場合，この環境ではdrbがインストールされていないということ．
    
    そのため，インストールする必要がある．
    
    最新バージョンのdrbをインストールするには，
    
    ```
    Copy codegem install drb
    
    ```
    
    ただし、エラーメッセージに指定のバージョンが書かれている場合，念のためそのバージョンをインストールするのがよいかもしれない．
    
    その場合は以下のように指定してインストールする
    
    ```
    Copy codegem install drb -v 2.0.6
    ```
    
    [drb | RubyGems.org | コミュニティのgemホスティングサービス](https://rubygems.org/gems/drb?locale=ja)
    
3. yarn のアップデート
    
    `yarn [set version](https://yarnpkg.com/cli/set/version) stable` で更新できる．
    
    以下の公式サイトを参考に
    
    [Installation | Yarn](https://yarnpkg.com/getting-started/install)
    
4. activesupportのインストール
    
    `gem install activesupport -v 6.1.7.7` 
    
    [activesupport | RubyGems.org | your community gem host](https://rubygems.org/gems/activesupport)
    
5. cocoapodsのインストール・PATH
    
    `sudo gem install cocoapods`

    公式サイト
    [CocoaPods.org](https://guides.cocoapods.org/using/getting-started.html#getting-started)
    
    .zshenvというファイルを開いて
    
    `export PATH=$HOME/.gem/bin:$PATH`
    
    というコードを書き込み保存する．
    
    .zshenvファイルがない場合
    
    ターミナルを開き，
    
    `touch .zshenv` で作る．
    
    そして，
    
    `open .zshenv` で開く．
    

## 最後に

いずれも最新状態でない可能性はありますが，最新状態にすると互換性がないという場合もありますので，最新状態にすることが常に正しいということはありません．

そのため，よくエラーメッセージをよんで，指定のバージョンを読み込むことが必要です．

加えて，エラーメッセージの解読に生成系AIに尋ねることはかなり有効でありますが，それだけでは全て解決できない場合がります．そのため，公式サイトの活用はかなり重要です！！

**AI**と **公式サイト**を上手に使いましょう！！

Flutter公式サイト
[Start building Flutter iOS apps on macOS](https://docs.flutter.dev/get-started/install/macos/mobile-ios?tab=download)
