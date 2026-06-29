---
slug: gcp-02
title: gcp_02
date: 2025-10-28 12:20:12
tags:
- google cloud
- google 
categories:
  - Note
---


GCP衝刺
==
1. Load balance 負載平衡器
{{< youtube ZskT0ZSEPEg >}}
2. GCP教學
https://youtube.com/playlist?list=PLvYsUzEf9kaP39bS21SKn4Onp3KQRbFsA
3. 
```
#! /bin/bash
sudo apt-get update
sudo apt-get install -y python3 python3-dev python3-pip
cd nsc-q2
export EXTERNAL_IP=34.110.254.140	
sed -i "s/EXTERNAL_IP/${EXTERNAL_IP}/I"' ./templates/index.html
pip3 install -r requirements.txt
export GOOGLE_APPLICATION_CREDENTIALS=
GOOGLE_APPLICATION_CREDENTIALS 
export DB_HOST= 
export DB_PORT= 
export DB_USER=
export DB_PASS=
export DB_NAME=test-q2-schema
export FLASK_APP=main.py
flask run -h 0.0.0.0 -p 80 &
```

任務一：使用Nginx 建立靜態網頁+VPC+SG
==


1. 建立執行個體 開80PORT
2. sudo apt-get update
3. sudo apt-get install nginx 
4. 使用自訂web資源放入nginx裏頭
*https://aws-tc-largeobjects.s3-us-west-2.amazonaws.com/ILT-TF-200-ACACAD-20-EN/Module-3-Challenge-Lab/static-website.zip*
```
1. cd /var/www/html
2. sudo apt-get install wget
3. sudo apt-get install unzip 
4. cd /var/www
5. sudo chmod 777 html 給html檔權限
6. cd /var/www/html
7. wget {網站zip}
8. unzip {網站zip}
9. 重新刷新葉面 就得到一個不安全http://咖非網頁
```
![](https://i.imgur.com/gvkRH0G.jpg)

-----

任務二：使用Nginx+Auto Scaling 建立ACA架構
==
![](https://i.imgur.com/GEdckxp.png)

1. 建立VPC
2. 建立子網
3. 建立Route table 
4. 建立 Internet gateway
5. 建立VPC 安全組
6. 建立 EC2
7. 建立RDS 
8. 建立 映像檔
9. 建立 目標群組(Target Group)
10. 建立 ALB LoadBalance 
11. 建立啟動組態
12. 建立 AutoScaling 



