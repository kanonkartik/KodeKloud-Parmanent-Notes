# Python Application Running on Server

## Cloning and Setting Up a Flask Application
```bash
cd /opt
sudo git clone https://github.com/mmumshad/simple-webapp-flask
cd simple-webapp-flask
sudo pip install -r requirements.txt
```

## Modifying and Running the Application
```bash
sudo sed -i 's/8080/5000/g' app.py
python3 app.py
```

## Running Flask App with Gunicorn
```bash
gunicorn app:app
```

## Running Flask App in Background
```bash
sudo sed -i 's/0.0.0.0/127.0.0.1/g;s/8080/5000/g' /opt/simple-webapp-flask/app.py
cd /opt/simple-webapp-flask/
nohup python3 app.py &
```

---

# Node.js Application Setup

## Cloning and Setting Up a Node.js Application
```bash
sudo git clone https://github.com/contentful/the-example-app.nodejs
cd the-example-app.nodejs
npm install
```

## Running the Node.js Application
```bash
node app.js
npm run start:dev
```

## Running with PM2 (Process Manager for Node.js)
```bash
sudo npm install pm2 -g
pm2 start app.js
pm2 start app.js -i 4 # Run with multiple instances
pm2 delete app.js # Stop and remove
```

---

# Database Setup (MariaDB / MySQL)

## MariaDB Setup
```bash
sudo systemctl start mariadb
sudo mysql
```

### Creating Database and User
```sql
CREATE DATABASE ecomdb;
CREATE USER 'ecomuser'@'localhost' IDENTIFIED BY 'ecompassword';
GRANT ALL PRIVILEGES ON *.* TO 'ecomuser'@'localhost';
FLUSH PRIVILEGES;
```

## MySQL Setup
```bash
mysql -u root -p
```

### Updating Password
```sql
SET PASSWORD = PASSWORD('P@ssw0rd123');
FLUSH PRIVILEGES;
```

---

# PHP and Apache Setup

## Installing Apache and PHP
```bash
sudo yum install -y httpd php php-mysqlnd
sudo systemctl start httpd
sudo systemctl enable httpd
```

## Setting PHP as Default Page
```bash
sudo sed -i 's/index.html/index.php/g' /etc/httpd/conf/httpd.conf
```

## Deploying an E-Commerce Application
```bash
sudo git clone https://github.com/kodekloudhub/learning-app-ecommerce.git /var/www/html/
sudo sed -i 's/172.20.1.101/localhost/g' /var/www/html/index.php
```

---

# GIT Basics

## Checking System Information
```bash
cat /etc/*release*
