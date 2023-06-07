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



