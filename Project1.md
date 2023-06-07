This project is to illustrate the implementation of LAMP stack technology which is the combination of the linux operating system, the apache webserver, mysql for the database to store our information and the langauage PHP. The combination of all these technology help to develop a software product. 

For this project, we need to have an aws account for our cloud infrastructure and from there we can use various kinds of linux operating systems that aws provides for use. A very good understanding of the linux command is highly needed for this project to be able to navigate through the terminal while configuring our webservers and databases.

First thing first is to log in to your aws account with the valid credentials then spin up an EC2 instance which is our virtual server or machine. 
<img width="1440" alt="Screenshot 2023-06-05 at 13 20 27" src="https://github.com/kelvinola/Devops-Training/assets/115745653/ccc050b9-e72e-418e-a320-10e6bd9b571c">

After clicking "launch an instance" give the instance a name and then select the kind of operating system that you want and in this case we would be using the ubuntu linux distro 


<img width="1440" alt="Screenshot 2023-06-05 at 13 29 40" src="https://github.com/kelvinola/Devops-Training/assets/115745653/10e5a0d3-903d-45e5-b2dd-f7e38ca03722">

create a keypair and for this instance for security reasons and download it to your computer. Create a security group for the firewall, allow ssh traffic from anywhere; make sure the number of instance is 1 and now you can finally launch the instance. 


<img width="1436" alt="Screenshot 2023-06-05 at 13 51 21" src="https://github.com/kelvinola/Devops-Training/assets/115745653/5df3e84f-3b33-4daf-914d-d0091062abd0">


now it is time to connect to our instance on our local machine or terminal

we can easily achieve that by selecting the instance that we launched and click the connect button whic will lead us to this page 


<img width="1440" alt="Screenshot 2023-06-05 at 14 05 01" src="https://github.com/kelvinola/Devops-Training/assets/115745653/c3fff3a6-bb60-48f9-9dd5-54b3ca2f9ffb">


copy what is under the example and save it somewhere so that you can paste it on to your local machine.

on your local machine, change your directory into the download folder where your keypair was downloaded into and paste the instance so that you can connect to your instance from your computer. 


<img width="1440" alt="Screenshot 2023-06-05 at 14 11 15" src="https://github.com/kelvinola/Devops-Training/assets/115745653/b7d0a5a7-3923-499a-a542-ff55ba550b2b">


now ive been able to connect to my virtual machine that was launch on aws in my personal computer's terminal.

the first thing to do after connecting to the terminal is to update the server using the $ sudo apt update

to avoid confusion, it is a good practice to name your server in order to differentiate the different works that you could be doing 



<img width="1440" alt="Screenshot 2023-06-05 at 14 21 22" src="https://github.com/kelvinola/Devops-Training/assets/115745653/7194ad79-65fa-4338-904e-ab526ced43e3">


Now it is time to dive into the real work!


STEP 1 INSTALLING APACHE SERVER 

The first thing is install our webserver annd for this project the webserver of choice is apache http server which is a widely used server software. it is a open source software the is available for free, it is fast, reliable and secure. 

Use $ sudo apt install apache2 to install apache 


<img width="1440" alt="Screenshot 2023-06-05 at 14 50 25" src="https://github.com/kelvinola/Devops-Training/assets/115745653/2e780689-eaac-4f74-aa37-93abe020a96b">


run sudo systemctl status apache2 to check the status of the webserver that had just been installed. 


<img width="1440" alt="Screenshot 2023-06-05 at 14 50 44" src="https://github.com/kelvinola/Devops-Training/assets/115745653/733f63a2-2fd2-4211-b73d-001117411961">

Our server is working fine which is a good sign that everything is going on good so far 

another way of ensuring that our webserver is running, is by copying the public ip of our virtual machine and run it on the internet browser to see if the apache page will come up but before we do that we have to make sure that our http port in our security group opened in order for the webpage to show 


<img width="1440" alt="Screenshot 2023-06-05 at 15 30 02" src="https://github.com/kelvinola/Devops-Training/assets/115745653/4f40ab50-31e0-4080-a5f4-f8c83cc81a66">



copy the publiic ip from aws and paste it to your web browser and add :80 behind the ip address and apache default page should come up.



<img width="1440" alt="Screenshot 2023-06-05 at 15 35 16" src="https://github.com/kelvinola/Devops-Training/assets/115745653/b6d2e7b1-0433-45b4-8959-b2813940a60f">


STEP 2 INSTALLING MYSQL 


now that my web server is running , the next thing to do is to install a database management system that will be able to store and manage our data for the website in a relational database. mysql is a very popular database management system which is used within the php envirnoment. 


i installed mysql with $ sudo apt install mysql-server

<img width="1440" alt="Screenshot 2023-06-05 at 19 54 14" src="https://github.com/kelvinola/Devops-Training/assets/115745653/fd2f3535-457a-4687-a7f5-3ee9920da4ac">


then run sudo mysql 


<img width="1440" alt="Screenshot 2023-06-05 at 20 09 14" src="https://github.com/kelvinola/Devops-Training/assets/115745653/cba53edb-9279-4e38-9484-a2cefddd73d9">



STEP 3 INSTALLING PHP 

PHP is the component of our setup that will process code to display dynamic content to the end user but in addition for the PHP to work we have to install the php-mysql which is the module that allows php to communicate with mysql based databases. the libapache2-mod-php module will enable apache to handle php files. 

to install php and the module  $ sudo apt install php libapache2-mod-php php-mysql


<img width="1440" alt="Screenshot 2023-06-05 at 20 22 49" src="https://github.com/kelvinola/Devops-Training/assets/115745653/740a56da-386e-47b7-82b5-0c46c0b7ac91">


To check what version of php you installed then use the php -v command 


<img width="1440" alt="Screenshot 2023-06-05 at 20 26 35" src="https://github.com/kelvinola/Devops-Training/assets/115745653/98c364b2-0630-4bc4-858e-18f1acf3f366">


STEP 4 Creating a virtual host for your website using apache

for this project, we will need to set up a domain called projectlamp. by default apache has one server block enabled but we will ignore that and add our own configurations by creating our own directory and call it projectlamp and change ownership of the directory using the chown command 


<img width="1440" alt="Screenshot 2023-06-05 at 21 12 28" src="https://github.com/kelvinola/Devops-Training/assets/115745653/d362ee49-a29c-47a7-aa26-aa514e257871">


Then, create and open a new configuration file in Apache’s sites-available directory using your preferred command-line editor.


<img width="1440" alt="Screenshot 2023-06-05 at 21 16 38" src="https://github.com/kelvinola/Devops-Training/assets/115745653/8284a686-195c-4547-90b6-cae8127ff33a">


With this VirtualHost configuration, we’re telling Apache to serve projectlamp using /var/www/projectlampl as its web root directory. If you would like to test Apache without a domain name, you can remove or comment out the options ServerName and ServerAlias by adding a # character in the beginning of each option’s lines. Adding the # character there will tell the program to skip processing the instructions on those lines.

You can now use a2ensite command to enable the new virtual host:

<img width="1440" alt="Screenshot 2023-06-05 at 21 27 18" src="https://github.com/kelvinola/Devops-Training/assets/115745653/2e1d772f-614f-4865-af30-ec562decbe43">


You might want to disable the default website that comes installed with Apache. This is required if you’re not using a custom domain name, because in this case Apache’s default configuration would overwrite your virtual host. To disable Apache’s default website use a2dissite command , type:


<img width="1440" alt="Screenshot 2023-06-05 at 21 30 59" src="https://github.com/kelvinola/Devops-Training/assets/115745653/e1532377-ea9e-4c24-8d3d-d58c51feed9a">


using the configtest command to make sure that the syntax is ok in the configuration 



<img width="1440" alt="Screenshot 2023-06-05 at 21 33 23" src="https://github.com/kelvinola/Devops-Training/assets/115745653/bbf3a21e-fb40-4e4d-a940-e90c7c1ca85a">


Finally, reload Apache so these changes take effect:

sudo systemctl reload apache2


Your new website is now active, but the web root /var/www/projectlamp is still empty. Create an index.html file in that location so that we can test that the virtual host works as expected:

sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html




<img width="1440" alt="Screenshot 2023-06-05 at 21 39 49" src="https://github.com/kelvinola/Devops-Training/assets/115745653/ea19d449-8684-4c44-8d16-b49db12e21f3">


STEP 5 ENABLING PHP ON THE WEBSITE 


With the default DirectoryIndex settings on Apache, a file named index.html will always take precedence over an index.php file. This is useful for setting up maintenance pages in PHP applications, by creating a temporary index.html file containing an informative message to visitors. Because this page will take precedence over the index.php page, it will then become the landing page for the application. Once maintenance is over, the index.html is renamed or removed from the document root, bringing back the regular application page.



In case you want to change this behavior, you’ll need to edit the /etc/apache2/mods-enabled/dir.conf file and change the order in which the index.php file is listed within the DirectoryIndex directive:

sudo vim /etc/apache2/mods-enabled/dir.conf



After saving and closing the file, you will need to reload Apache so the changes take effect:

sudo systemctl reload apache2
Finally, we will create a PHP script to test that PHP is correctly installed and configured on your server.

Now that you have a custom location to host your website’s files and folders, we’ll create a PHP test script to confirm that Apache is able to handle and process requests for PHP files.

Create a new file named index.php inside your custom web root folder:

vim /var/www/projectlamp/index.php
This will open a blank file. Add the following text, which is valid PHP code, inside the file:



<?php
phpinfo();



This page provides information about your server from the perspective of PHP. It is useful for debugging and to ensure that your settings are being applied correctly.




If you can see this page in your browser, then your PHP installation is working as expected.




After checking the relevant information about your PHP server through that page, it’s best to remove the file you created as it contains sensitive information about your PHP environment -and your Ubuntu server. You can use rm to do so:




sudo rm /var/www/projectlamp/index.php


You can always recreate this page if you need to access the information again later.



<img width="1440" alt="Screenshot 2023-06-05 at 21 50 23" src="https://github.com/kelvinola/Devops-Training/assets/115745653/08ef960f-7cf7-4424-b1cf-e59fe2e1d7a3">











