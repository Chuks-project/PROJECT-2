#WEB STACK IMPLEMENTATION (LEMP STACK)
--------------------------------------
In this project you will implement a similar stack as in project-one, but with an alternative Web Server – NGINX, which is also very popular and widely used by many websites in the Internet

##Step 0 – Preparing prerequisites
In order to complete this project you will need an AWS account and a virtual server with Ubuntu Server OS. This can be achieved by following the step 0 of project-one.

My Visual Studio Code(VSC) is connected by copying the following link from my AWS EC2 Dashboard "ssh -i "vicky.pem" ubuntu@ec2-54-157-5-131.compute-1.amazonaws.com" as can be seen below:


![Configuring Nginx to use PHP Processor](https://user-images.githubusercontent.com/65022146/188306961-b47cf75f-125e-44ae-9014-03796eaf391a.png)


## STEP 1 – INSTALLING THE NGINX WEB SERVER
In project-one we used Apache as our webserver. An alternative is Nginx. Nginx is known for its ability to handle multiple open connections effectively.

- To Update your server’s package index run the command below: 
  sudo apt update
  
 - To install Nginx run the command below:
    sudo apt install nginx
    
  - To verify that nginx was successfully installed and is running as a service in Ubuntu, run:
   sudo systemctl status nginx
   
   - If the Server is active and running, it will appear same as the image below:
   
   ![Sudo Systemctl](https://user-images.githubusercontent.com/65022146/189503229-41731e9e-306b-4afd-88fd-904b7c42d311.png)
