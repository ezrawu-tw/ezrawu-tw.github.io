---
slug: linux-build-safety-wordpress
title: linux_build_safety_wordpress
date: 2025-10-28 12:31:14
tags: 
- Linux
- WordPress

categories:
  - Note
---
slug: linux-build-safety-wordpress

# Linux 建立安全性wordpress
0. 安全群組
1. ![](https://i.imgur.com/DjVEpt7.png) 20 21 22 80 443


ubuntu 環境建立
1.安裝 Apache Web Server (Step One: Installing apache web server)
```
sudo apt-get update
sudo apt-get install apache2
```

2.安裝MySql
```
sudo apt-get install mysql-server
sudo mysql_secure_installation
```
忘記密碼:
```
sudo mysql

ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```


3.安裝phpMyAdmin
`sudo apt install phpmyadmin`

4.安裝wordpress
```
sudo apt-get install unzip #安裝解壓縮軟體
cd /var/www/html #跑到資料夾底下
sudo  rm -r index.html #刪除index.html 
sudo wget https://tw.wordpress.org/wordpress-4.9-zh_TW.zip 
sudo unzip wordpress-4.9-zh_TW.zip
sudo mv /var/www/html/wordpress/* /var/www/html
cd ..
sudo chmod 777 html
#圖片上傳->先進到
/var/www/html/wordpress
sudo chmod 777 wp-content
```
![](https://i.imgur.com/wavkzsd.png)

5.設定動態位址域名
6.新增安全性憑證
```
sudo add-apt-repository ppa:certbot/certbot #增加程式支援庫
sudo apt-get update #更新
sudo apt-get install python-certbot-apache #安裝
sudo certbot --apache
```
到domin name 地方輸入自己的動態網域(No ip)

Certbot 會根據掃描結果列出所有的網域，可以選擇多個，建議直接按 Enter就會替所有網域都安裝憑證 # 接者會問要不要將所有的 HTTP Request 全部重導向到 HTTPS，建議選擇 2 全部轉
安裝後確認
可以利用 SSL Labs 的 SSL Test  測試你的網站是否正確安裝了 SSL 憑證
Certbot 預設會啟動自動更新，輸入以下指令確認自動更新有沒有正常執行
sudo systemctl status certbot.timer

輸入自己網域名，清除瀏覽器快取

7.ftp遠端傳輸
按站台管理員
先打開putty
```
#到跟目錄 
cd /var/www/html
#建立資料夾 
sudo mkdir webftp
#給權限  
sudo chmod 777 webftp/
#然後再新增站台 主機ip/(自己網域名)變為機器ip
#改進階設定 
/var/www/html/webftp
```
![](https://i.imgur.com/39f2S6k.png)

![](https://i.imgur.com/R8K8Pbo.png)
![](https://i.imgur.com/TrrsAKe.png)

 
















