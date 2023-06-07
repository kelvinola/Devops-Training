LEMP Implementation. 


This project is basically the same as project 1 but this time around a different webserver called nginx is begin used to serve our webbpage to the public. 


After launching the instance and connecting to the instance from your local computer, it is always a good practice to update your server using the sudo apt update command 


<img width="1440" alt="Screenshot 2023-06-07 at 12 59 26" src="https://github.com/kelvinola/Devops-Training/assets/115745653/e416927a-30bb-4682-8ecf-c1d82d3bc48e">


Then use the sudo apt install nginx -y to install nginx iinto your virtual server and the -y is there to answer yes for any question that might come up while installing the webserver. 



<img width="1440" alt="Screenshot 2023-06-07 at 13 00 25" src="https://github.com/kelvinola/Devops-Training/assets/115745653/e5eea5f6-79cf-47d3-b7a0-c94ebe581e90">


After the installation has been completed, it also a good practice to check the status of your webserver to check whether it is active and running by using the sudo systemctl status nginx 


<img width="1440" alt="Screenshot 2023-06-07 at 13 01 21" src="https://github.com/kelvinola/Devops-Training/assets/115745653/593e9fd0-68ba-45e2-b79a-17736ee6ed38">

For the page to be able to show on the internet browser, we need to open port 80 in our securuity group on aws 


<img width="1440" alt="Screenshot 2023-06-07 at 13 31 53" src="https://github.com/kelvinola/Devops-Training/assets/115745653/a53ce088-8a0b-4f1f-9c05-47cfacb1e9c9">


After opening the port 80, You can copy the public ip address from aws and paste it into your internet browser and the nginx page should come up like this 
