# 第4回　課題

・vpcの作成

<img width="999" alt="スクリーンショット 2022-11-12 10 25 24" src="https://user-images.githubusercontent.com/102453302/201450945-199e57a6-ecd8-4306-8a13-58929ba00d13.png">


-第4回の資料を参考にしながら作成



　・EC2の作成
 
 <img width="1009" alt="スクリーンショット 2022-11-12 10 53 03" src="https://user-images.githubusercontent.com/102453302/201451021-dd6fa185-83ff-41f8-8712-cfe038c121d7.png">



<img width="1005" alt="スクリーンショット 2022-11-12 10 27 34" src="https://user-images.githubusercontent.com/102453302/201451033-93522810-b45c-43e2-8e02-708353cd37e6.png">


 
-第4回の資料を参考にしながら作成


・RDSの作成

<img width="910" alt="スクリーンショット 2022-11-12 10 30 50" src="https://user-images.githubusercontent.com/102453302/201451116-ba29aec4-e57b-4b92-8066-02d90de56903.png">


<img width="1280" alt="スクリーンショット 2022-11-12 10 31 38" src="https://user-images.githubusercontent.com/102453302/201451127-f76f5076-f369-4600-8338-20336b291cc0.png">


<img width="1200" alt="スクリーンショット 2022-11-12 10 32 26" src="https://user-images.githubusercontent.com/102453302/201451141-f23e2231-eb85-4b22-906e-fc0b2697a2e0.png">


・EC2にSSH接続成功

<img width="1080" alt="スクリーンショット 2022-11-12 10 34 11" src="https://user-images.githubusercontent.com/102453302/201451198-12539b72-7b61-4e9f-9867-7f49708e3c24.png">

＊躓きポイント
キーペア作成の際に記号を入れてしまい認証が上手く行かなかった。再度インスタンスから作成し、記号を除いたキーペアを作成し解決
　ダウンロードしたpemファイルを使用する

### 参考サイト

- [パスの表示参考](https://tcd-theme.com/2020/11/mac-file-path.html)

- [接続に関するサイト](https://zenn.dev/valentiiii46/articles/dd87b085782bd5)


・EC2からRDSへの接続

<img width="857" alt="スクリーンショット 2022-11-12 10 34 32" src="https://user-images.githubusercontent.com/102453302/201451652-313453f2-aeda-4963-be49-a60f5f9f0d4a.png">

- [参考サイト](https://qiita.com/OPySPGcLYpJE0Tc/items/0fc95a6b865f6bb89179)



#### 躓きポイント

mysqlに接続できずに何回もエラーが出てしまったが原因はRDSの設定項目の中の「マスターパスワード確認」という項目が空白であったこと
初歩的な原因で何日も彷徨ってしまった
