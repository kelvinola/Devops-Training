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
