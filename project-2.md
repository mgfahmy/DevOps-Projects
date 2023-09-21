## WEB STACK IMPLEMENTATION (LEMP STACK)
### STEP 1 – INSTALLING THE NGINX WEB SERVER
## Steps
##### 1- sudo apt update
##### 2- sudo apt install nginx -y
##### 3- sudo systemctl status nginx
##### 4- curl http://localhost:80

### STEP 2 — INSTALLING MYSQL
## Steps
##### 1- sudo apt install mysql-server
##### 2- sudo mysql
#####    mysql> exit

### STEP 3 – INSTALLING PHP
## Steps
##### sudo apt install php-fpm php-mysql -y

### STEP 4 — CONFIGURING NGINX TO USE PHP PROCESSOR
## Steps
##### 1- sudo mkdir /var/www/projectLEMP
##### 2- sudo nano /etc/nginx/sites-available/projectLEMP
##### server {
#####    listen 80;
#####    server_name projectLEMP www.projectLEMP;
#####    root /var/www/projectLEMP;

#####    index index.html index.htm index.php;

#####    location / {
#####        try_files $uri $uri/ =404;
#####    }

#####    location ~ \.php$ {
#####        include snippets/fastcgi-php.conf;
#####        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
#####     }

#####    location ~ /\.ht {
#####        deny all;
#####    }
##### }
##### 3- sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/
##### 4- sudo nginx -t
##### 5- sudo unlink /etc/nginx/sites-enabled/default
##### 6- sudo systemctl reload nginx
##### 7- sudo vim index.html

![Project2pix12](https://user-images.githubusercontent.com/121172005/269735388-34b6577b-3f54-4fbf-9635-fcd827db68f8.PNG)

### STEP 5 – RETRIEVING DATA FROM MYSQL DATABASE WITH PHP 
## Steps
##### 1- sudo mysql
##### mysql> create database example_database;
##### mysql> create user 'example_user'@'%' identified with mysql_native_password by 'password';
##### mysql> grant all on example_database.* to 'example_user'@'%';
##### mysql> exit
##### 2-  mysql -u example_user -p
##### 3- mysql> show databases;
##### mysql> create table example_database.todo_list (
##### -> item_id int auto_increment,
##### -> content varchar(255),
##### -> primary key(item_id)
##### -> );
##### mysql> insert into example_database.todo_list (content) values ("my first important item");
##### mysql> insert into example_database.todo_list (content) values ("my second important item");
##### mysql> insert into example_database.todo_list (content) values ("my third important item");
##### mysql> insert into example_database.todo_list (content) values ("help me get one more");
##### mysql> select * from example_database.todo_list;
##### mysql> exit
##### 4- sudo nano /var/www/projectLEMP/todo_list.php
##### <?php
##### $user = "example_user";
##### $password = "password";
##### $database = "example_database";
##### $table = "todo_list";
#####
##### try {
#####   $db = new PDO("mysql:host=localhost;dbname=$database", $user, $password);
#####   echo "<h2>TODO</h2><ol>";
#####   foreach($db->query("SELECT content FROM $table") as $row) {
#####     echo "<li>" . $row['content'] . "</li>";
#####   }
#####   echo "</ol>";
##### } catch (PDOException $e) {
#####     print "Error!: " . $e->getMessage() . "<br/>";
#####     die();
##### }
![Project2pix23](https://user-images.githubusercontent.com/121172005/269735172-70c3b147-d0d0-4047-a3af-22f479b50285.PNG)
##### Access this page in the web browser http://<Public_domain_or_IP>/todo_list.php**
![Project2pix26](https://user-images.githubusercontent.com/121172005/269735703-33f27c43-89e5-484f-a82b-afefee8c1ff7.PNG)

