1-Signed up for an AWS account.
2-Logged in as IAM user
3-In the VPC console, I create Security Group
4-Launched an EC2 instance
5-I selelected the Ubuntu free tier instance
6-I set the required configurations (Enabled public IP, security group, and key pair) and finally launched the instance.
7-Next I SSH into the instance using Windows Terminal
8-in cmd i enter "ssh -i ".ssh\mgfahmy.pem" ubuntu@ec2-16-16-211-80.eu-north-1.compute.amazonaws.com"
9- sudo apt update -y
10- sudo apt install apache2 -y
11- sudo systemctl status apache2
12- curl http://localhost:80
13- sudo apt install mysql-server
14- sudo mysql
mysql> alter user 'root'@'localhost' identified with mysql_native_password by 'PassWord.1';
mysql> exit
15-  sudo apt install php libapache2-mod-php php-mysql -y
16- sudo mkdir /var/www/projectlamp
17- sudo chown -R $USER:$USER /var/www/projectlamp
18- sudo vi /etc/apache2/sites-available/projectlamp.conf
<VirtualHost *:80>
ServerName projectlamp
ServerAlias www.projectlamp
ServerAdmin webmaster@localhost
DocumentRoot /var/www/projectlamp
ErrorLog ${APACHE_LOG_DIR}/error.log
CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
19- sudo a2ensite projectlamp 
20- sudo a2dissite 000-default
21- sudo apche2ctl configtest
22- sudo systemctl reload apache2
23- cd /var/www/projectlamp/
24- git clone https://github.com/elmoatasem112/static-website-example.git
https://user-images.githubusercontent.com/121172005/269292374-ba32576f-cf24-43d8-b070-17ab0bdc14e4.PNG
https://user-images.githubusercontent.com/121172005/269288612-95fd68dc-c5b5-45f4-8e5e-446787b00c6d.png
