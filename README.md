# LAMP環境を作成するまで
centos6.10 ,mysql 5.6.50 ,php7.3.10  
おいおいcloudformationのテンプレートとかpulumiなどupできたらと思う。

# 1．AWSでインスタンス作成
AWSにログインし
```
EC2->インスタンスの作成->AWS Marketplace->Centos6で検索
```
以下のインスタンスを選択する。
![Test Image 1](img/centos.PNG)



# 2．centos6.10初期設定
rootパスワード設定
```bash
$sudo su -
$passwd
```
リポジトリの向き先が古いので変更
```bash
$sudo sed -i -e "s|mirror\.centos\.org/centos/\$releasever|vault\.centos\.org/6.6|g" /etc/yum.repos.d/CentOS-Base.repo
$sudo sed -i -e "s|#baseurl=|baseurl=|g" /etc/yum.repos.d/CentOS-Base.repo
$sudo sed -i -e "s|mirrorlist=|#mirrorlist=|g" /etc/yum.repos.d/CentOS-Base.repo
```
更新
```bash
$sudo yum update
```

# 3．mysql5.6.50インストール
インストール、初期起動に追加、起動、バージョン確認
```bash
$sudo yum -y install http://dev.mysql.com/get/mysql-community-release-el6-5.noarch.rpm
$sudo yum -y install mysql-community-server
$sudo chkconfig mysqld on
$sudo service mysqld start
$mysql --version
```
初期設定～rootで接続まではここを参考
https://www.server-world.info/query?os=CentOS_6&p=mysql

ユーザ作成と任意のIPから接続できるDBを作成
※IP制限はAWSのセキュリティグループにて行う
```
CREATE USER 'username'@'%' IDENTIFIED BY 'userpassword';
DROP USER 'username'@'%';
CREATE DATABASE dbname;
GRANT ALL PRIVILEGES ON dbname.* TO 'username'@'%';
```
権限の確認(これで全部yになっていることを確認)
```
SELECT * FROM mysql.db WHERE user = 'username' AND host = '%' AND db = 'dbname' \G
```
