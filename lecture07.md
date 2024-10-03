## 　第7回：システムのセキリュティについての感想


AWSにはセキリュティサービスが充実しており、それを組み合わせることで高レベルのセキュリティシステムを構築することができる。

セキュリティは非常に重要なセクションになるので任せられるエンジニアになるには経験と知識が必須である。

今回学習したAWSのセキュリティサービスは以下の通りである

- Amazon CodeGuru CodeGuru Reviewer

AI を用いて GitHubなどのリポジトリにあるコードをスキャンし、改善を提案してくれる。

料金もそれなりに掛かる

- AWS Firewall Manager  WAF（Web Application Firewall）

ファイアウォール

- AWS Certificate Manager（ACM） 

SSL 証明書を発行するマネージドサービス

- Amazon Inspector

脆弱性のスキャンを行うサービス

- AWS Security Hub

AWS の設定情報を検索して、脆弱な部分を指摘してくれたり、特定の業界基準に準拠しているかを確認してくれる

- AWS Key Management Service（KMS）

暗号鍵マネージドサービス

- Secrets Manager 

秘匿しなければいけない情報を KMS で暗号化して安全に保管、呼び出しするサービス


- AWS Shield 

DDoS攻撃からインフラを保護してくれるマネージドサービスであり、DDoS 攻撃と思われる通信を自動で遮断してくれる

Standard と Advanced の 2 プランあり、AWS ではそれぞれ Shield Standard、Shield Advancedと呼ばれている

Advanced では Standard の内容に加え、以下の内容が提供されます。その代わり超高額（3000 ドル/月で 12 ヶ月縛り）

基本的には Standard で事足ります。Advanced の有効化は簡単にできてしまうので、基本的にはページにも行かないこと

- IAM Access Analyzer 

各種ポリシーのチェックを行い、大きな権限を与えていないかを確認してくれる

- Amazon GuardDuty

AWS 内のイベントをチェックし、セキュリティインシデントの疑いがあるイベントについて指摘してくれる

- Amazon Macie

S3バケットに個人情報やクレジットカード番号など機密情報が含まれないかを検知する

- Detective

複数の AWS サービスを横断して、セキュリティインシデントの発生元などを特定するための GUIを提供する

- AWS Network Firawall

インターネットゲートウェイと VPC の境界に設置するファイアーウォールを実現するサービス


- コストとセキュリティ

セキュリティサービスがこれだけあるので、何でも実装してしまうとコストが膨大に掛かってしまう。

何かあると怖いからと思って全て実装することは現実的ではないので適材適所にサービスに実装できるセキュリティ知識と経験を得られるようにしていきたい。

セキュリティは身近に存在しており、自分のawsアカウントも例外ではない。

- アカウント乗っ取り
- ウィルス感染
- DDos攻撃

等のリスクが考えられる

- [DDos攻撃について](https://www.stylez.co.jp/columns/ddos_prevention_in_aws/)

- [その他の脅威](https://kurojica.com/server/blog/3176/)

