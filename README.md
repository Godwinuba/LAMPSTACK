# LAMPSTACK
Lampstack project
# PROJECT 1
## WEB STACK IMPLEMENTATION (LAMP STACK) IN AWS
### Welcome to your very first PBL Project
You must be really excited to start getting your hands dirty. There is a lot of projects ahead, so without any delay, lest get started.

## Step 1
### Launch an Ec2 instance of t2.micro with ubuntu server 20.04 LTS (HVM)
1.	AWS account setup and Provisioning an Ubuntu Server
2.	Connecting to your EC2 Instance
Or follow the instructions below.
1.	Register a new AWS account following this instruction.
2.	Select your preferred region (the closest to you) and launch a new EC2 instance of t2.micro family with Ubuntu Server 20.04 LTS (HVM)
![screenshot1](./iMAGES/screenshot-20240627-112220.png)
# SSH into the ubuntu instance
-  Both Putty and ssh use the SSH protocol to establish connectivity between computers. It is the most secure protocol because it uses crypto algorithms to encrypt the data that is transmitted – it uses TCP port 22 which is open for all newly created EC2 instances in AWS by default
-	Change directory into the location where your PEM file is. Most likely will be in the Downloads folder
- `cd Download`
- 	Change permissions for the private key file (.pem), otherwise you can get an error “Bad permission
- `sudo chmod 0400 <private-key-name>. pem`
connect instance by runnning:
`ssh -i <private-key-name>. pem ubuntu@<Public-IP-address>`
![screeshot2](./iMAGES/screenshot2.png)


## Step 2: INSTALLING APACHE AND UPDATING THE FIREWALL
Apache is an open-source software available for free. It runs on 67% of all webservers in the world. It is fast, reliable, and secure. It can be highly customized to meet the needs of many different environments by using extensions and modules. Most WordPress hosting providers use Apache as their web server software.
- Install Apache using Ubuntu’s package manager ‘apt’
 1. #Update a list of packages in package manager
`sudo apt update`
2. #Run apache2 package installation
`sudo apt install apache2`
- To verify that apache2 is running as a Service in our OS, use following command
`sudo systemctl status apache2`
*If it is green and running, then you did everything correctly – you have just launched your first Web Server in the Clouds!*
![screenshot4](./iMAGES/screenshot-4.png)

Our server is running and we can access it locally and from the Internet (Source 0.0.0.0/0 means ‘from any IP address’).

First, let us try to check how we can access it locally in our Ubuntu shell, run:
``curl http://localhost:80``
or	
 ``curl http://127.0.0.1:80``

Open a web browser of your choice and try to access following url
``http://<Public-IP-Address>:80``
![APACHE](./iMAGES/Apache.png)

## STEP 3 — INSTALLING MYSQL
Now that you have a web server up and running, you need to install a Database Management System (DBMS) to be able to store and manage data for your site in a relational database

- Again, use ‘apt’ to acquire and install this software:
 `sudo apt install mysql-server -y`
 When the installation is finished, log in to the MySQL console by typing:
 `sudo mysql`
 This will connect to the MySQL server as the administrative database user root, which is inferred by the use of sudo when running this command You should see output like this:
 ![MY SQL](./iMAGES/MY%20SQL.png)

 - It’s recommended that you run a security script that comes pre-installed with MySQL. This script will remove some insecure default settings and lock down access to your database system.
`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';`
- exit the MYSQL shell with mysql> `exit` 
- start the interacting script by running:
`sudo mysql_secure_installation -y`

- When you’re finished, test if you’re able to log in to the MySQL console by typing:
 `sudo mysql -p`
- To exit the MySQL console, type:
mysql> `exit`

# STEP 4 — INSTALLING PHP
PHP is the component of our setup that will process code to display dynamic content to the end user. In addition to the php package, you’ll need php-mysql, a PHP module that allows PHP to communicate with MySQL-based databases. You’ll also need libapache2-mod-php to enable Apache to handle PHP files.

To install these 3 packages at once, run:
`sudo apt install php libapache2-mod-php php-mysql`
Once the installation is finished, you can run the following command to confirm your PHP version:
`php -v`
![php version](./iMAGES/php%20version.png)

# STEP 5 — CREATING A VIRTUAL HOST FOR YOUR WEBSITE USING APACHE

Apache on Ubuntu 20.04 has one server block enabled by default that is configured to serve documents from the /var/www/html directory. 
We will leave this configuration as is and will add our own directory next next to the default one.
Create the directory for projectlamp using ‘mkdir’ command as follows:
`sudo mkdir /var/www/projectlamp`
Next, assign ownership of the directory with your current system user:
 `sudo chown -R $USER:$USER /var/www/projectlamp`
 Then, create and open a new configuration file in Apache’s sites-available directory using your preferred command-line editor. Here, we’ll be using Nano
 sudo nano /etc/apache2/sites-available/projectlamp.conf

`sudo vi /etc/apache2/sites-available/projectlamp.conf`
This will create a new blank file. Paste in the following bare-bones configuration by hitting on i on the keyboard to enter the insert mode, and paste the text.

vim /var/www/projectlamp/index.php
This will open a blank file. Add the following text, which is valid PHP code, inside the file:
<?php
phpinfo();
