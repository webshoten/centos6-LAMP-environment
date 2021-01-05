# LAMP環境を作成するまで
centos6.10 ,mysql 5.6.31 ,php7.3.10  

# 1．AWSでインスタンス作成
AWSにログインし
```
EC2->インスタンスの作成->AWS Marketplace->Centos6で検索
```
以下のインスタンスを選択する。
![Test Image 1](img/centos.PNG)



# 2．centos6初期設定
rootパスワード設定
```bash
$sudo su -
$passwd
```
