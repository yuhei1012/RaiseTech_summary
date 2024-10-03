ELBの追加

# 参考サイト
https://zenn.dev/ito110/scraps/5031f7ce7b92cf

https://dev.classmethod.jp/articles/sales-ec2-elb-session/

https://nishinatoshiharu.com/ec2-with-alb-setting/#_EC2nginx

エラー時の閲覧サイト
https://zenn.dev/tikka/articles/6109990725a0f417d058


# ロードバランサーの　DNSNameをブラウザに入力後

![img](lecture05/ロードバランサー導入.png)



# ロードバランサー追加時にハマったエラー

・ターゲットグループのHealth statusでunhealthy

![img](lecture05/img:ロードバランサー導入時のエラー1.png)

![image](lecture05/img:ロードバランサー導入時エラー2.png)

# エラー解消
設定後にnginxとunicornを再起動してみたらhealthyとなり解消した
*再起動をしないでエラーコードを延々調べて時間を要してしまった。

https://github.com/yuhei1012/RaiseTech_summary/blob/1e5a1de4080787e78ba4687c3b9540e6987ceb9a/lecture05_ELB%E8%BF%BD%E5%8A%A0.md
