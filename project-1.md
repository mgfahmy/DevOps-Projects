## WEB STACK IMPLEMENTATION (LAMP STACK) IN AWS
### ASW account setup and provisioning an Ubuntu Server
## Steps
### 1-Signed up for an AWS account.
### 2-Logged in as IAM user
3-In the VPC console, I create Security Group
4-Launched an EC2 instance
5-I selelected the Ubuntu free tier instance
6-I set the required configurations (Enabled public IP, security group, and key pair) and finally launched the instance.
7-Next I SSH into the instance using Windows Terminal
8-in cmd i enter "ssh -i ".ssh\mgfahmy.pem" ubuntu@ec2-16-16-211-80.eu-north-1.compute.amazonaws.com"

### INSTALLING APACHE AND UPDATING THE FIREWALL
#### Steps
1- sudo apt update -y
2- sudo apt install apache2 -y
3- sudo systemctl status apache2
4- curl http://localhost:80



### INSTALLING MYSQL
#### Steps
1-sudo apt install mysql-server
2- sudo mysql
mysql> alter user 'root'@'localhost' identified with mysql_native_password by 'PassWord.1';
mysql> exit

### STEP 3 — INSTALLING PHP
#### Steps
1. To install these 3 packages at once, run:
**sudo apt install php libapache2-mod-php php-mysql**
**php -v**


### STEP 4 — CREATING A VIRTUAL HOST FOR YOUR WEBSITE USING APACHE
#### Steps
1. Setting up a domain called projectlamp. Create the directory for projectlamp using ‘mkdir’. Run: **sudo mkdir /var/www/projectlamp**
2. assign ownership of the directory with your current system user, run: **sudo chown -R $USER:$USER /var/www/projectlamp**
3. Next, create and open a new configuration file in Apache’s sites-available directory. Tpye: **sudo vi /etc/apache2/sites-available/projectlamp.conf**
4. This will create a new blank file. Paste in the following bare-bones configuration by hitting on i on the keyboard to enter the insert mode, and paste the text:
**<VirtualHost *:80>
    ServerName projectlamp
    ServerAlias www.projectlamp 
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/projectlamp
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
  </VirtualHost>**
  ![Project1pix15](https://user-images.githubusercontent.com/74002629/176587989-12ed00f0-f3c5-482f-98dc-1e9c849e8a99.PNG)
  
  5.To save and close the file. Hit the esc button on the keyboard, Type :, Type wq. w for write and q for quit and Hit ENTER to save the file.
  6. use the ls command to show the new file in the sites-available directory: **sudo ls /etc/apache2/sites-available**
  ![Project1pix16](https://user-images.githubusercontent.com/74002629/176588144-f7413246-cf7e-43df-8399-cd7c81e98bae.PNG)
  
  7. Next, use a2ensite command to enable the new virtual host: **sudo a2ensite projectlamp**
  8. Disable the default website that comes installed with Apache. type: **sudo a2dissite 000-default**
  9. Esure your configuration file doesn’t contain syntax errors, run: **sudo apache2ctl configtest**
  10. Finally, reload Apache so these changes take effect: **sudo systemctl reload apache2**
  ![Project1pix17](https://user-images.githubusercontent.com/74002629/176588441-b562f1be-f86d-4c35-83a9-1d0294d9eae0.PNG)
  
  12. The website is active, but the web root /var/www/projectlamp is still empty. Create an index.html file in that location so that we can test that the virtual host works as expected:
**sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html**
12. Relaod the public IP to see changes to the apache2 default page.
![Project1pix19](https://user-images.githubusercontent.com/74002629/176588537-7e43b408-6674-4530-afa8-7e65c69800e8.PNG)

### STEP 5 — ENABLE PHP ON THE WEBSITE
#### Steps
1. With the default DirectoryIndex settings on Apache, a file named index.html will always take precedence over an index.php file. To make index.php file tak precedence need to edit the /etc/apache2/mods-enabled/dir.conf file and change the order in which the index.php file is listed within the DirectoryIndex directive.
2. Run: **sudo vim /etc/apache2/mods-enabled/dir.conf** then:
**<IfModule mod_dir.c>
        #Change this:
        #DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
        #To this:
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>**
4. Save and close file.
5. Next, reload Apache so the changes take effect, type: **sudo systemctl reload apache2**
6. Finally, we will create a PHP script to test that PHP is correctly installed and configured on your server. Create a new file named index.php inside the custom web root folder, run: **vim /var/www/projectlamp/index.php**
7. This will open a blank file. Add the PHP code: 
**<?php
phpinfo();**
8. Save and close the file, then refresh the page to see changes.
9. ![Project1pix20](https://user-images.githubusercontent.com/74002629/176642095-d8dbb3b8-ba7f-4772-89d9-6d54c42f35a0.PNG)
