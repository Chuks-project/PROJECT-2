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

  - Using a curl command, and on port 80, check and test if Nginx can handle request locally on our Ubuntu shell, run:
  
     curl http://localhost:80
       or
     curl http://127.0.0.1:80
     
    - Also confirm that Nginx can handle request from the internet by lunching it on the browser using the URL below:

       http://<Public-IP-Address>:80
       
    - Public-IP-Address can be accessed from the EC2 Insatnce
    
    - An image as seen below will appear on your browser if the Nginx is running(being able to receice and handle requsts from the Internet):
    
  
      ![Welcome to Nginx](https://user-images.githubusercontent.com/65022146/189514562-cf1ef9b1-1a05-4227-9a46-0a87f11fa164.png)
      
      
      
      
      
      
      Step 2 — Installing MySQL
      
    - Run the command below to install mysql:
    
       sudo apt install mysql-server
       
    
    - When prompted, confirm installation by typing Y, and then ENTER.
     
     
     
    - To secure your database run the preinstalled script below:
      
         sudo mysql_secure_installation
         
     - Confirm that you have access to the database by running the command below:

           sudo mysql

     - Exit the database with the command below:

          exit
          
      - The commands above are reprsented in the image below as:
     
     
     ![sudo install and secure1](https://user-images.githubusercontent.com/65022146/189516088-72cf0c2d-ff6c-4103-bb9e-0a7010303916.png)
     
     
     
     ![sql Done](https://user-images.githubusercontent.com/65022146/189516127-6fe8aa26-e88b-42e4-b122-2e9389f6c187.png)
     
     
     
     ![Mysql secure Installation and Sudo Mysql ](https://user-images.githubusercontent.com/65022146/189516158-9188d69b-cd68-498c-9f2b-3c958260f6f4.png)

     


      
         
