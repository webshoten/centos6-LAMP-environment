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
リポジトリの向き先が古いので変更
```
sudo sed -i -e "s|mirror\.centos\.org/centos/\$releasever|vault\.centos\.org/6.6|g" /etc/yum.repos.d/CentOS-Base.repo
sudo sed -i -e "s|#baseurl=|baseurl=|g" /etc/yum.repos.d/CentOS-Base.repo
sudo sed -i -e "s|mirrorlist=|#mirrorlist=|g" /etc/yum.repos.d/CentOS-Base.repo
```
