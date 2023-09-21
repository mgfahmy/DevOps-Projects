## WEB STACK IMPLEMENTATION (LAMP STACK) IN AWS
### ASW account setup and provisioning an Ubuntu Server
## Steps
##### 1-Signed up for an AWS account.
##### 2-Logged in as IAM user
##### 3-In the VPC console, I create Security Group
##### 4-Launched an EC2 instance
##### 5-I selelected the Ubuntu free tier instance
##### 6-I set the required configurations (Enabled public IP, security group, and key pair) and finally launched the instance.
##### 7-Next I SSH into the instance using Windows Terminal
##### 8-in cmd i enter "ssh -i ".ssh\mgfahmy.pem" ubuntu@ec2-16-16-211-80.eu-north-1.compute.amazonaws.com"

### INSTALLING APACHE AND UPDATING THE FIREWALL
## Steps
##### 1- sudo apt update -y
##### 2- sudo apt install apache2 -y
##### 3- sudo systemctl status apache2
##### 4- curl http://localhost:80

### INSTALLING MYSQL
## Steps
##### 1-sudo apt install mysql-server
##### 2- sudo mysql
##### mysql> alter user 'root'@'localhost' identified with mysql_native_password by 'PassWord.1';
##### mysql> exit

### STEP 3 — INSTALLING PHP
## Steps
##### 1. To install these 3 packages at once, run: sudo apt install php libapache2-mod-php php-mysql
##### 2. php -v**


### STEP 4 — CREATING A VIRTUAL HOST FOR YOUR WEBSITE USING APACHE
## Steps
##### 1- sudo vi /etc/apache2/sites-available/projectlamp.conf
##### <VirtualHost *:80>
##### ServerName projectlamp
##### ServerAlias www.projectlamp
##### ServerAdmin webmaster@localhost
##### DocumentRoot /var/www/projectlamp
##### ErrorLog ${APACHE_LOG_DIR}/error.log
##### CustomLog ${APACHE_LOG_DIR}/access.log combined
##### </VirtualHost>
##### 2- sudo a2ensite projectlamp 
##### 3- sudo a2dissite 000-default
##### 4- sudo apche2ctl configtest
##### 5- sudo systemctl reload apache2

### STEP 5 — release WEBSITE
## Steps
##### 1- cd /var/www/projectlamp/
##### 2- git clone https://github.com/elmoatasem112/static-website-example.git
 ![Project1pix20](https://user-images.githubusercontent.com/121172005/269292374-ba32576f-cf24-43d8-b070-17ab0bdc14e4.PNG)
![Project1pix20](https://user-images.githubusercontent.com/121172005/269288612-95fd68dc-c5b5-45f4-8e5e-446787b00c6d.png)
