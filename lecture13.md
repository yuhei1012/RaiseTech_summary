# 第13回　CircleCiを活用した自動化

- [CircleCiログイン画面](https://circleci.com/vcs-authorize/?lang=ja&returnTo=)

- [使用したconfig.yml](.circleci/config.yml)
- [Ansible実行フォルダ](Ansible)
- [Serverspec実行フォルダ](serverspec)

- [＊参考になったコマンド、参照URL](lecture13/lecture13/使用コマンド及び参照URL一覧)
  
- CI/CDツールを使用してセットアップから構築、デプロイ、serverspecを使用してテスト実行までを自動化

- CircleCiを使用しCFnでリソースを作成、作成されたリソースにAnsibleでRails環境とアプリケーションのセットアップ、最後にserverspecでテストを実行する構成となる。

- アクセスキーやパスワードの記述が必要になるためセキュリティ、ハードコーティングの観点からCircleCiのEnvironment Variables(環境変数)機能は必須となる。


### CircleCiでの作成画面

![img](lecture13/lecture13/CircleCi_Succsess.png)




### CFn成功

![img](lecture13/lecture13/CircleCi_CFn_Succsess.png)


### Ansible成功

![img](lecture13/lecture13/CircleCi_Ansible_Success.png)


### Serverspec成功

![img](lecture13/lecture13/CircleCi_Serverspec_Succsess.png)

### アプリケーション画像確認
![img](lecture13/lecture13/CircleCi_S3_画像.png)

##### 　ハマったポイント

- Pumaの起動でハマってしまった。
Pumaが起動しないのは自分の経験上ファイル構文に問題がある場合が多い。大抵はそこを修正すると動く。
development.rb、puma.rb、puma.serviceこの内のどれかに問題がある。


Puma起動エラー
![img](lecture13/lecture13/Puma起動エラー.png)

Pumaブラウザアクセスエラー
![imag](lecture13/lecture13/Pumaエラー時_ブラウザアクセス.png)

Puma起動成功


![img](lecture13/lecture13/Puma起動成功.png)

### アプリケーションをブラウザからアクセスした時画像が表示されない。

画像の保存先をAmazon S3にしている構成だがブラウザからアクセスした時に画像が表示されないことがある。
"config.active_storage.variant_processor = :mini_magick"をapplication.rbに追記し
RAILS_ENV=development bundle exec rails assets:precompileを実行する構文にすること。
precompileを実行するコマンドがないとapplication.rbに記述されなかった。
playbookに直接記述するよりもテンプレート(development.rb.j2)を使用するのが有効であった。
ImageMagickのインストールやminimagickをGemfileに追加する構文も必須である。

##### development.rbの記述にも注意が必要である。
- config.active_storage.service = :amazon→表示される
- config.active_storage.service = :local→表示されない

 
必要な記述と更新ができないとブラウザからアクセスすると下記のようになる。

![ブラウザからアクセスした時アプリケーションが表示されない](lecture13/lecture13/Railsアプリケーション画像表示エラー.png)


- Serverspecの項目では.ssh/configの設定が以前の課題のものになっておりssh接続でのエラーが出続けた。
そこの設定を今回の課題のものにし、テストが実行された。

- インデントのずれによる構文エラーが多かった。



## 総括
今回の課題はかなりの時間を要することとなり、難しい課題であった。
最初はlocalでAnsibleを成功させるところから始めたが、これも中々うまくいかず苦労をした。
しかしできてしまえば10分程で作成、デプロイ、テストが実行できるので非常に便利なツールであると感じた。
業務として使用できるレベルではないのでまだまだ学習は継続していきたい。

### 構成の流れ


この図の構成では、CircleCIのプロジェクトがAnsibleのコントロールノードとして機能しています。具体的には、CircleCIがCI/CDパイプラインを実行する際に、Ansibleを用いてEC2インスタンス（ターゲットノード）にリモート接続し、設定やデプロイを行う役割を果たしている。

以下のような流れとなる：

1. GitHubにコードがプッシュされる: これがCircleCIのビルドプロセスをトリガーします。
2. CircleCiがジョブを実行: CircleCi上のパイプラインの一環として、Ansibleが起動します。この時点で、CircleCiの環境（CircleCiのプロジェクト）自体がAnsibleのコントロールノードとして動作。
3. Ansibleがターゲットノードに接続: CircleCi上のAnsibleは、設定されたEC2インスタンスにSSHなどを使って接続し、アプリケーションのセットアップや設定（NginxやRailsの構築）を行う。したがって、CircleCiのジョブがコントロールノードの役割を担い、EC2インスタンスがAnsibleの指示に従って構成されるという流れである。

これにより、開発者は手動でEC2にログインして設定を行う必要がなくなり、コードがプッシュされるたびにCircleCIが自動的にインフラを構成・デプロイすることとなる。




# 構成図
![img](lecture13/lecture13/構成図_lecture13_修正_S3.png)


## CircleCiでAnsible、Serverspecまで実行する際の注意点
このリポジトリーのファイルを引用して同じことをする際は以下の点を変更すること。
- inventoryファイルのipアドレスを変更すること
- EC2のPublic_IPアドレスを変更すること
- S3のバケット名を変更すること。又は削除しておくこと。
- CircleCiの環境変数を変更すること
  AWSアクセスキーやシークレットアクセスキーを新たに作成、登録すること。
  変更の必要がなければ同じものでも可
- .circleciフォルダのconfig.yml構文にあるCFnのパスやAnsibleのパスは適宜変更する
  
![img](lecture13/lecture13/環境変数登録_CircleCi.png)

- RDSは環境変数にパスワードとDB名を登録しているので、CFnの作成が終了したら一度中断してパスワードとDB名をCircleCiに登録してから実行するとエラーは起こらない。
  これは、RDSだけでなくEC2やS3に言えるのでCFn作成までのCircleCiに留めておき、必要な環境変数を登録したらDeploy～Testまでのワークフローにすると良い。

#### 環境変数を登録したので次回からはCircleCiの環境変数とSSH Keysを変更すれば自動でデプロイからテストまで実行できる。
  

#### 今回登録した環境変数

CircleCiに環境変数を登録する際は大文字が基本となる。
- AWS_ACCESS_KEY_ID
- AWS_SECRET_ACCESS_KEY
- AWS_DEFAULT_REGION
- AWS_DNS
- DB_USERNAME
- DB_HOST (これはRDSのエンドポイント)
- DB_PASSWORD
- EC2_PUBLIC_IP
- SSH_KEY_PATH(pemファイル名)
- S3_BACKET_NAME
- AWS_REGION

#### その他注意点
- .ssh/configのhost(ipアドレス)を変更すること
  ＊今回はローカルにpemファイルをダウンロードしたのでローカルの.ssh/configを変更した。
- templaetsファイルはvarsを使用していないので下記のような形式で直接CircleCiから環境変数を定義している。
  
region(テンプレート内の表記): "{{ lookup('env', 'CircleCiに登録した変数名') }}

*'env',の隣は半角スペースを忘れないこと。ナミカッコ{}の前後も半角スペースを一つ空ける

````
S3_storage.yml.j2

amazon:
  service: S3
  region: "{{ lookup('env', 'AWS_REGION') }}
  bucket: "{{ lookup('env', 'S3_BACKET_NAME') }}"

local:
  service: Disk
  root: <%= Rails.root.join("storage") %>


database.yml.j2

default: &default
  adapter: mysql2
  encoding: utf8mb4
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  username: "{{ lookup('env', 'DB_USERNAME') }}"
  password: "{{ lookup('env', 'DB_PASSWORD') }}"
  host: "{{ lookup('env', 'DB_HOST') }}"

development:
  <<: *default
  database: raisetech_live8_sample_app_development


````



- その他

  
Githubプロテクションルール

![img](lecture13/lecture13/Github_保護ルール.png)



