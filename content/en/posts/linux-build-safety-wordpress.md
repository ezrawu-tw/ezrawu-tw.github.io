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

# Building a Secure WordPress Site on Linux
0. Security Group
1. ![](https://i.imgur.com/DjVEpt7.png) Ports: 20, 21, 22, 80, 443


Setting up the Ubuntu environment:
1. Install Apache Web Server (Step One: Installing Apache Web Server)
```
sudo apt-get update
sudo apt-get install apache2
```

2. Install MySQL
```
sudo apt-get install mysql-server
sudo mysql_secure_installation
```
Forgot your password:
```
sudo mysql

ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```


3. Install phpMyAdmin
`sudo apt install phpmyadmin`

4. Install WordPress
```
sudo apt-get install unzip  # install decompression software
cd /var/www/html            # navigate to the directory
sudo  rm -r index.html      # delete index.html
sudo wget https://tw.wordpress.org/wordpress-4.9-zh_TW.zip 
sudo unzip wordpress-4.9-zh_TW.zip
sudo mv /var/www/html/wordpress/* /var/www/html
cd ..
sudo chmod 777 html
# For image uploads -> first go to
/var/www/html/wordpress
sudo chmod 777 wp-content
```
![](https://i.imgur.com/wavkzsd.png)

5. Configure a dynamic domain name
6. Add an SSL certificate
```
sudo add-apt-repository ppa:certbot/certbot  # add the PPA repository
sudo apt-get update                           # update
sudo apt-get install python-certbot-apache    # install
sudo certbot --apache
```
Enter your dynamic domain name (e.g., from No-IP) when prompted.

Certbot will list all detected domains based on its scan. You can select multiple; it is recommended to press Enter to install certificates for all domains. It will then ask whether to redirect all HTTP requests to HTTPS — it is recommended to choose option 2 to redirect all traffic.

After installation, verify the result:
You can use SSL Labs' SSL Test to verify that your site has the SSL certificate correctly installed.
Certbot enables auto-renewal by default. Run the following command to confirm auto-renewal is working properly:
sudo systemctl status certbot.timer

Enter your domain name and clear your browser cache.

7. FTP remote file transfer
Open the Site Manager.
First open PuTTY:
```
# Navigate to the root directory
cd /var/www/html
# Create a folder
sudo mkdir webftp
# Grant permissions
sudo chmod 777 webftp/
# Then add a new site with the host IP (your domain name) pointing to the machine IP
# Change the advanced setting remote directory to:
/var/www/html/webftp
```
![](https://i.imgur.com/39f2S6k.png)

![](https://i.imgur.com/R8K8Pbo.png)
![](https://i.imgur.com/TrrsAKe.png)

 
