# lecture03 課題

## サンプルアプリケーション起動

#### [サンプルコード](https://github.com/yuta-ushijima/raisetech-live8-sample-app)

<img width="1280" alt="スクリーンショット 2022-10-19 22 40 13" src="https://user-images.githubusercontent.com/102453302/196717253-4eb952f5-e65f-4521-96dd-9870a44e4657.png">

## APサーバー終了時
 
 <img width="1279" alt="スクリーンショット 2022-10-19 22 38 31" src="https://user-images.githubusercontent.com/102453302/196717711-f90b939f-757c-43e5-8049-5df8a0d2509a.png">


## DB サーバー終了時
  
- [参考サイト](https://26gram.com/start-stop-mysql)
  
<img width="1275" alt="スクリーンショット 2022-10-19 22 13 09" src="https://user-images.githubusercontent.com/102453302/196718017-d333c187-612f-4920-b427-1ddc48a7b2d2.png">


### AP サーバーの名前とバージョンを確認

-APサーバー名　puma

-コマンド:puma -v

* Puma version: 5.6.4 (ruby 2.6.3-p62) ("Birdie's Version")
*  Min threads: 5
*  Max threads: 5
*  Environment: development
*          PID: 5289
* Listening on http://0.0.0.0:8080　

### DB サーバー名とバージョン

-DBサーバー名　:mysql

-バージョン:mysql  Ver 8.0.31 for Linux on x86_64 (MySQL Community Server - GPL)

-コマンド: mysql --version

### Rails の構成管理ツールの名前
-bundle

-コマンド:bundle -v

-Bundler version 2.3.24


#総括
2週目ということもあり講座の内容が前回よりも理解度が多少上がったのか頭に入ってきた。
カリキュラムに多少の変更はあれどアプリケーションのデプロイは前回もやっていたのでスムーズに行けた。
環境構築に関しては改めてがっちり作っておかないとちょっとしたことでエラーになると実感した。
今回はYAMLの構成エラーが発生して少し焦った。原因としてはスペースが足りない所が一つあっただけであった。
一度経験したことを再度確認しながら進められることは非常に有意義であった。

