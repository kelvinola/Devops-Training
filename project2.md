LEMP Implementation. 

This project is basically the same as project 1 but this time around a different webserver called nginx is begin used to serve our webbpage to the public. 


After launching the instance and connecting to the instance from your local computer, it is always a good practice to update your server using the sudo apt update command 


STEP 1

<img width="1440" alt="Screenshot 2023-06-07 at 12 59 26" src="https://github.com/kelvinola/Devops-Training/assets/115745653/e416927a-30bb-4682-8ecf-c1d82d3bc48e">


Then use the sudo apt install nginx -y to install nginx iinto your virtual server and the -y is there to answer yes for any question that might come up while installing the webserver. 


<img width="1440" alt="Screenshot 2023-06-07 at 13 00 25" src="https://github.com/kelvinola/Devops-Training/assets/115745653/e5eea5f6-79cf-47d3-b7a0-c94ebe581e90">


After the installation has been completed, it also a good practice to check the status of your webserver to check whether it is active and running by using the sudo systemctl status nginx 


<img width="1440" alt="Screenshot 2023-06-07 at 13 01 21" src="https://github.com/kelvinola/Devops-Training/assets/115745653/593e9fd0-68ba-45e2-b79a-17736ee6ed38">

For the page to be able to show on the internet browser, we need to open port 80 in our securuity group on aws 


<img width="1440" alt="Screenshot 2023-06-07 at 13 31 53" src="https://github.com/kelvinola/Devops-Training/assets/115745653/a53ce088-8a0b-4f1f-9c05-47cfacb1e9c9">


After opening the port 80, You can copy the public ip address from aws and paste it into your internet browser and the nginx page should come up like this 

![Screenshot 2023-06-07 at 13 40 06 (2)](https://github.com/kelvinola/Devops-Training/assets/115745653/30df246b-ded7-4000-ae21-ee39cbc348da)


STEP 2


Now that our webserver is up and running, it is now time to install our database that will keep our information and data 



<img width="1440" alt="Screenshot 2023-06-07 at 13 54 36" src="https://github.com/kelvinola/Devops-Training/assets/115745653/f1459379-f999-4419-8c1c-117b8af31c01">


after installing mysql, you will need to create a root user and give the root a password for access, after that exit from mysql 


<img width="1440" alt="Screenshot 2023-06-07 at 13 58 50" src="https://github.com/kelvinola/Devops-Training/assets/115745653/7f38a54f-0fcb-416b-81f9-bcd107d7de5b">


STEP 3


You have Nginx installed to serve your content and MySQL installed to store and manage your data. Now you can install PHP to process code and generate dynamic content for the web server.

While Apache embeds the PHP interpreter in each request, Nginx requires an external program to handle PHP processing and act as a bridge between the PHP interpreter itself and the web server. This allows for a better overall performance in most PHP-based websites, but it requires additional configuration. You’ll need to install php-fpm, which stands for “PHP fastCGI process manager”, and tell Nginx to pass PHP requests to this software for processing. Additionally, you’ll need php-mysql, a PHP module that allows PHP to communicate with MySQL-based databases. Core PHP packages will automatically be installed as dependencies.

To install these 2 packages at once, run:

sudo apt install php-fpm php-mysql


<img width="1440" alt="Screenshot 2023-06-07 at 14 12 06" src="https://github.com/kelvinola/Devops-Training/assets/115745653/57b91d6d-1885-4680-803c-df57b2a06159">


Step 4 — Configuring Nginx to Use PHP Processor
When using the Nginx web server, we can create server blocks (similar to virtual hosts in Apache) to encapsulate configuration details and host more than one domain on a single server. In this guide, we will use projectLEMP as an example domain name.

On Ubuntu 20.04, Nginx has one server block enabled by default and is configured to serve documents out of a directory at /var/www/html. While this works well for a single site, it can become difficult to manage if you are hosting multiple sites. Instead of modifying /var/www/html, we’ll create a directory structure within /var/www for the your_domain website, leaving /var/www/html in place as the default directory to be served if a client request does not match any other sites.


Create the root web directory for your_domain as follows:

sudo mkdir /var/www/projectLEMP
Next, assign ownership of the directory with the $USER environment variable, which will reference your current system user:

sudo chown -R $USER:$USER /var/www/projectLEMP
Then, open a new configuration file in Nginx’s sites-available directory using your preferred command-line editor. Here, we’ll use nano:

sudo nano /etc/nginx/sites-available/projectLEMP
This will create a new blank file. Paste in the following bare-bones configuration:

#/etc/nginx/sites-available/projectLEMP

server {
    listen 80;
    server_name projectLEMP www.projectLEMP;
    root /var/www/projectLEMP;

    index index.html index.htm index.php;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
     }

    location ~ /\.ht {
        deny all;
    }

}

When you’re done editing, save and close the file. If you’re using nano, you can do so by typing CTRL+X and then y and ENTER to confirm.

Activate your configuration by linking to the config file from Nginx’s sites-enabled directory:

sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/
This will tell Nginx to use the configuration next time it is reloaded. You can test your configuration for syntax errors by typing:

sudo nginx -t
You shall see following message:

nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
If any errors are reported, go back to your configuration file to review its contents before continuing.

We also need to disable default Nginx host that is currently configured to listen on port 80, for this run:

sudo unlink /etc/nginx/sites-enabled/default
When you are ready, reload Nginx to apply the changes:

sudo systemctl reload nginx
Your new website is now active, but the web root /var/www/projectLEMP is still empty. Create an index.html file in that location so that we can test that your new server block works as expected:

sudo echo 'Hello LEMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectLEMP/index.html
Now go to your browser and try to open your website URL using IP address:

http://<Public-IP-Address>:80
  
  
<img width="1440" alt="Screenshot 2023-06-07 at 14 27 00" src="https://github.com/kelvinola/Devops-Training/assets/115745653/217854da-c29f-45d6-b61d-de401d27529e">
    
    
![Screenshot 2023-06-07 at 14 28 13 (2)](https://github.com/kelvinola/Devops-Training/assets/115745653/b43f7fe9-54b4-48b7-bc35-89273605b6c9)

    
You can leave this file in place as a temporary landing page for your application until you set up an index.php file to replace it. Once you do that, remember to remove or rename the index.html file from your document root, as it would take precedence over an index.php file by default.


Your LEMP stack is now fully configured. In the next step, we’ll create a PHP script to test that Nginx is in fact able to handle .php files within your newly configured website.
    
          
Step 5 – Testing PHP with Nginx
Your LEMP stack should now be completely set up.

At this point, your LAMP stack is completely installed and fully operational.

You can test it to validate that Nginx can correctly hand .php files off to your PHP processor.

You can do this by creating a test PHP file in your document root. Open a new file called info.php within your document root in your text editor:

sudo nano /var/www/projectLEMP/info.php
    

Type or paste the following lines into the new file. This is valid PHP code that will return information about your server:

<?php
phpinfo();
You can now access this page in your web browser by visiting the domain name or public IP address you’ve set up in your Nginx configuration file, followed by /info.php:

http://`server_domain_or_IP`/info.php
You will see a web page containing detailed information about your server:

<img width="1440" alt="Screenshot 2023-06-07 at 14 35 28" src="https://github.com/kelvinola/Devops-Training/assets/115745653/2b85fe1a-4f51-40e8-ab15-c30a92577e80">


![Screenshot 2023-06-07 at 14 35 28 (2)](https://github.com/kelvinola/Devops-Training/assets/115745653/f0004116-d704-4efe-89a1-de6fa116b532)


Step 6 — Retrieving data from MySQL database with PHP
In this step you will create a test database (DB) with simple “To do list” and configure access to it, so the Nginx website would be able to query data from the DB and display it.

At the time of this writing, the native MySQL PHP library mysqlnd doesn’t support caching_sha2_authentication, the default authentication method for MySQL 8. We’ll need to create a new user with the mysql_native_password authentication method in order to be able to connect to the MySQL database from PHP.

We will create a database named example_database and a user named example_user, but you can replace these names with different values.

First, connect to the MySQL console using the root account:

sudo mysql
To create a new database, run the following command from your MySQL console:

mysql> CREATE DATABASE `example_database`;
Now you can create a new user and grant him full privileges on the database you have just created.

The following command creates a new user named example_user, using mysql_native_password as default authentication method. We’re defining this user’s password as password, but you should replace this value with a secure password of your own choosing.

mysql>  CREATE USER 'example_user'@'%' IDENTIFIED WITH mysql_native_password BY 'password';
Now we need to give this user permission over the example_database database:

mysql> GRANT ALL ON example_database.* TO 'example_user'@'%';
This will give the example_user user full privileges over the example_database database, while preventing this user from creating or modifying other databases on your server.

Now exit the MySQL shell with:


mysql> exit
You can test if the new user has the proper permissions by logging in to the MySQL console again, this time using the custom user credentials:


mysql -u example_user -p
Notice the -p flag in this command, which will prompt you for the password used when creating the example_user user. After logging in to the MySQL console, confirm that you have access to the example_database database:


mysql> SHOW DATABASES;

This will give you the following output:



Output
+--------------------+
| Database           |
+--------------------+
| example_database   |
| information_schema |
+--------------------+
2 rows in set (0.000 sec)
Next, we’ll create a test table named todo_list. From the MySQL console, run the following statement:




CREATE TABLE example_database.todo_list (item_id INT AUTO_INCREMENT,content VARCHAR(255),PRIMARY KEY(item_id));
Insert a few rows of content in the test table. You might want to repeat the next command a few times, using different VALUES:

mysql> INSERT INTO example_database.todo_list (content) VALUES ("My first important item");
To confirm that the data was successfully saved to your table, run:

mysql>  SELECT * FROM example_database.todo_list;
You’ll see the following output:

Output
+---------+--------------------------+
| item_id | content                  |
+---------+--------------------------+
|       1 | My first important item  |
|       2 | My second important item |
|       3 | My third important item  |
|       4 | and this one more thing  |
+---------+--------------------------+
4 rows in set (0.000 sec)
After confirming that you have valid data in your test table, you can exit the MySQL console:

mysql> exit
