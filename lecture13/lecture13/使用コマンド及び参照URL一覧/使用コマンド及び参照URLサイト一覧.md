- ansibleドライランコマンド
  
$ ansible-playbook -u ec2-user -i inventory --private-key ~/.ssh/pmeキー名 playbook.yml --check


--checkを外すと実際に走る


- nginxのrolesを作成したコマンド


$ ansible-galaxy init nginx --init-path=roles

- このコマンドでrolesにrubyのディレクトリを作成

  
$ ansible-galaxy init roles/ruby



- playbookにハイフンを使用するとsyntaxエラーになる可能性が高い。使うならアンダーバーが好ましい

- 下記のように検索するとtemplate_modulenについて公式ドキュメントで確認できる

  
  検索ワード：ansible template module
  

  [ansible template module](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/template_module.html)


- [ansibleでruby環境構築　参照URL](https://qiita.com/fukushi_yoshikazu/items/69debbdab621ee0a19c2)

- S3への画像保存及び画像ビューに必要なパッケージ

 GraphicsMagick（画像の表示用）

 
$ sudo amazon-linux-extras install GraphicsMagick1.3

config/application.rb ←ここに追記


→config.active_storage.variant_processor = :mini_magick


このようなエラーだと何かが無い、前のtasksでインストールされているはずのものが無い、等のエラーが多い
たくさんあるからと困惑しないように

tal: [3.112.233.245]: FAILED! => {"changed": true, "cmd": "source /etc/profile.d/rbenv.sh\nbundle install --deployment --without development test\n", "delta": "0:00:06.362056", "end": "2024-09-10 00:13:05.743777", "msg": "non-zero return code", "rc": 5, "start": "2024-09-10 00:12:59.381721", "stderr": "[DEPRECATED] The --deployment flag is deprecated because it relies on being remembered across bundler invocations, which bundler will no longer do in future versions. Instead please use bundle config set --local deployment 'true', and stop using this flag\n[DEPRECATED] The --without flag is deprecated because it relies on being remembered across bundler invocations, which bundler will no longer do in future versions. Instead please use bundle config set --local without 'development test', and stop using this flag\nDon't run Bundler as root. Bundler can ask for sudo if it is needed, and\ninstalling your bundle as root will break this application for all non-root\nusers on thi

- 一つのrolesだけ実行するにはplaybookにtagを記述する
- 実行コマンド　$ ansible-playbook playbook.yml -i inventory --tags rails_app

````
---
- name: Ensure Ruby is installed (using rbenv)
  shell: |
    source /etc/profile.d/rbenv.sh
    rbenv install -s 3.1.2
  args:
    creates: /usr/local/rbenv/versions/3.1.2
  tags: rails_app

- name: Set global Ruby version
  shell: |
    source /etc/profile.d/rbenv.sh
    rbenv global 3.1.2
  tags: rails_app
````

- その他参照URL
- [権限設定](https://qiita.com/Kyohei-takiyama/items/6dd6a7009618aba59207)
- [権限設定2](https://qiita.com/ir-yk/items/af8550fea92b5c5f7fca)
- [scpコマンド参照URL](https://japan.zdnet.com/article/35189624/)
- [serverspec_sshサイト](https://hitolog.blog/2021/10/14/serverspec/)
- [puma.service](https://engineer-daily.com/ec2-puma-setting/)
- [puma systemd登録](https://zenn.dev/trysmr/articles/65a6db4deffdbf)
- [ansibleインストール](https://hitolog.blog/2021/10/12/how-to-install-ansible/)
- [CFn → Ansible → Serverspec構築](https://qiita.com/taishin/items/89b42106582a2aa5495b)
- [ansible_デプロイ](https://qiita.com/masainaba921/items/e29c5b548e2e7b41b68b)
- [CircleCiについて](https://qiita.com/hika7719/items/20d01c4bc56bf09dec5c)
- [CircleCiについて2](https://qiita.com/gold-kou/items/4c7e62434af455e977c2)
- [CircleCi公式ドキュメント](https://circleci.com/docs/ja/hello-world/)
- [CircleCi_CFn_ハードコーティング解消_AZ](https://dev.classmethod.jp/articles/cfn-availavility-zone-notation/)
- [EC2_Ansible手動構築](https://hitolog.blog/2021/10/12/how-to-install-ansible/)
- [serverspec1](https://qiita.com/hitomatagi/items/12f9f10ff8e95dbe0999)
- [serverspec2](https://qiita.com/minamijoyo/items/467ddd13c0cab15330bf)
- [serverspec3](https://qiita.com/hitomatagi/items/956a8893aea6cb18a93f)
- [Linuxポート疎通確認](https://qiita.com/WisteriaWave/items/1e86a9d9488ee777c0a3)
- [アクセスキー、シークレットアクセスキーの作成](https://qiita.com/yamasakk/items/3060d22faeed8e05ebe4)



- mysqlとEC2接続コマンド

  
$ mysql -h [エンドポイント] -P 3306 -u admin -p
