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
slug: gcp-02

GCP Sprint
==
1. Load Balancer
{{< youtube ZskT0ZSEPEg >}}
2. GCP Tutorial
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

Task 1: Build a Static Website with Nginx + VPC + Security Group
==


1. Create an instance and open port 80
2. sudo apt-get update
3. sudo apt-get install nginx 
4. Use custom web resources placed inside nginx
*https://aws-tc-largeobjects.s3-us-west-2.amazonaws.com/ILT-TF-200-ACACAD-20-EN/Module-3-Challenge-Lab/static-website.zip*
```
1. cd /var/www/html
2. sudo apt-get install wget
3. sudo apt-get install unzip 
4. cd /var/www
5. sudo chmod 777 html  # grant permissions to the html directory
6. cd /var/www/html
7. wget {website-zip-url}
8. unzip {website-zip-file}
9. Refresh the page and you'll get an insecure http:// coffee shop website
```
![](https://i.imgur.com/gvkRH0G.jpg)

-----

Task 2: Build an ACA Architecture with Nginx + Auto Scaling
==
![](https://i.imgur.com/GEdckxp.png)

1. Create a VPC
2. Create subnets
3. Create a Route Table
4. Create an Internet Gateway
5. Create a VPC Security Group
6. Create an EC2 instance
7. Create an RDS instance
8. Create an AMI (image)
9. Create a Target Group
10. Create an ALB Load Balancer
11. Create a Launch Configuration
12. Create an Auto Scaling Group


