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
      
      
      
      
      
      
      # Step 2 — Installing MySQL
      
 - Run the command below to install mysql:
    
       sudo apt install mysql-server
       
    
 - When prompted, confirm installation by typing Y, and then ENTER.
     
     
     
 - To secure your database run the preinstalled script below:
      
         sudo mysql_secure_installation
         
 - Confirm that you have access to the database by running the command below:

           sudo mysql

 - Exit the database with the command below:

          exit
          
 - The commands above are reprsented in the images below as:
     
     
     ![sudo install and secure1](https://user-images.githubusercontent.com/65022146/189516088-72cf0c2d-ff6c-4103-bb9e-0a7010303916.png)
     
     
     
     ![sql Done](https://user-images.githubusercontent.com/65022146/189516127-6fe8aa26-e88b-42e4-b122-2e9389f6c187.png)
     
     
     
     ![Mysql secure Installation and Sudo Mysql ](https://user-images.githubusercontent.com/65022146/189516158-9188d69b-cd68-498c-9f2b-3c958260f6f4.png)
     
     
     
     
 # Step 3 – Installing PHP
 
 While Apache embeds the PHP interpreter in each request, Nginx requires an external program to handle PHP processing and act as a bridge between the PHP interpreter itself and the web server. This allows for a better overall performance in most PHP-based websites, but it requires additional configuration. You’ll need to install php-fpm, which stands for “PHP fastCGI process manager”, and tell Nginx to pass PHP requests to this software for processing. Additionally, you’ll need php-mysql, a PHP module that allows PHP to communicate with MySQL-based databases. Core PHP packages will automatically be installed as dependencies.

- To install these 2 packages at once, run:

     sudo apt install php-fpm php-mysql

  When prompted, type Y and press ENTER to confirm installation.
  
  
  
  
  # Step 4 — Configuring Nginx to Use PHP Processor
  
  When using the Nginx web server, we can create server blocks (similar to virtual hosts in Apache) to encapsulate configuration details and host more than one domain on a single server. In this guide, we will use projectLEMP as an example domain name.

On Ubuntu 20.04, Nginx has one server block enabled by default and is configured to serve documents out of a directory at /var/www/html. While this works well for a single site, it can become difficult to manage if you are hosting multiple sites. Instead of modifying /var/www/html, we’ll create a directory structure within /var/www for the your_domain website, leaving /var/www/html in place as the default directory to be served if a client request does not match any other sites.


- Create the root web directory for your_domain as follows:

   sudo mkdir /var/www/projectLEMP

- Set logged-in user as the owner of the directory /var/www/projectLEMP/

     sudo chown -R $USER:$USER /var/www/projectLEMP

- open a new configuration file in Nginx’s sites-available directory using your preferred command-line editor.

    sudo nano /etc/nginx/sites-available/projectLEMP
    
    
    
- This will create a new blank file. Paste in the following bare-bones configuration:


server { listen 80; server_name projectLEMP www.projectLEMP; root /var/www/projectLEMP;

index index.html index.htm index.php;

location / { try_files $uri $uri/ =404; }

location ~ .php$ { include snippets/fastcgi-php.conf; fastcgi_pass unix:/var/run/php/php7.4-fpm.sock; }

location ~ /.ht { deny all; }

}




Here’s what each of these directives and location blocks do:

- listen — Defines what port Nginx will listen on. In this case, it will listen on port 80, the default port for HTTP. root — Defines the document root where the files served by this website are stored. index — Defines in which order Nginx will prioritize index files for this website. It is a common practice to list index.html files with a higher precedence than index.php files to allow for quickly setting up a maintenance landing page in PHP applications. You can adjust these settings to better suit your application needs. server_name — Defines which domain names and/or IP addresses this server block should respond for. Point this directive to your server’s domain name or public IP address.

- location / — The first location block includes a try_files directive, which checks for the existence of files or directories matching a URI request. If Nginx cannot find the appropriate resource, it will return a 404 error.

- location ~ .php$ — This location block handles the actual PHP processing by pointing Nginx to the fastcgi-php.conf configuration file and the php7.4-fpm.sock file, which declares what socket is associated with php-fpm.

- location ~ /.ht — The last location block deals with .htaccess files, which Nginx does not process. By adding the deny all directive, if any .htaccess files happen to find their way into the document root ,they will not be served to visitors.

- When you’re done editing, save and close the file. If you’re using nano, you can do so by typing CTRL+X and then y and ENTER to confirm.

- Activate your configuration by linking to the config file from Nginx’s sites-enabled directory:

     sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/

- You can test your configuration for syntax errors by typing:

     sudo nginx -t

-  You shall see following message:

nginx: the configuration file /etc/nginx/nginx.conf syntax is ok

nginx: configuration file /etc/nginx/nginx.conf test is successful

- Disable default Nginx host that is currently configured to listen on port 80, for this run:

    sudo unlink /etc/nginx/sites-enabled/default

- Reload Nginx to apply the changes:

    sudo systemctl reload nginx

- Your new website is now active, but the web root /var/www/projectLEMP is still empty. Create an index.html file in that location so that we can test that your new server block works as expected:

sudo echo 'Hello LEMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectLEMP/index.html

- Now go to your browser and try to open your website URL using IP address:

    http://<Public-IP-Address>:80



 

 
 ![Hello lemp from Hostname](https://user-images.githubusercontent.com/65022146/189530859-3f548b96-0119-4676-84ff-2a8ae95300d7.png)
 
 
 - As seen above, the text from ‘echo’ command you wrote to index.html file, means your Nginx site is working as expected.
 
 
 
 
 
 # Step 5 – Testing PHP with Nginx

 Your LEMP stack should now be completely set up.

At this point, your LAMP stack is completely installed and fully operational.

You can test it to validate that Nginx can correctly hand .php files off to your PHP processor.

You can do this by creating a test PHP file in your document root. 

 - Open a new file called info.php within your document root in your text editor:

     sudo nano /var/www/projectLEMP/info.php

 = Type or paste the following lines into the new file. 
    <?php
    phpinfo();

- You can access your website with the Url below:

     ttp://server_domain_or_IP/info.php

- You will see a web page containing detailed information about your server as seen in the image below:

   
    ![Testing Nginx with PHP](https://user-images.githubusercontent.com/65022146/189535233-e1888232-6220-4077-b5a8-794b5dcce167.png)


- The image above contains sensitive information of your environment. So it is standard practice to remove it. Run the command below:

     sudo rm /var/www/your_domain/info.php



## Step 6 — Retrieving data from MySQL database with PHP

In this step you will create a test database (DB) with simple "To do list" and configure access to it, so the Nginx website would be able to query data from the DB and display it.

= First, connect to the MySQL console using the root account:

   sudo mysql

- To create a new database, run the following command from your MySQL console:

    mysql> CREATE DATABASE 'example_database';

- To Create a user and password run the command below:

    mysql> CREATE USER 'example_user'@'%' IDENTIFIED WITH mysql_native_password BY 'password';

- Now we need to give this user permission over the example_database database:

   mysql> GRANT ALL ON example_database.* TO 'example_user'@'%';

- To exit mysql as root user, run the command below:

   mysql> exit

- To test our database, log in as user: example_user using the command below:

mysql -u example_user -p

change into `example_database using the command below:

mysql> SHOW DATABASES;

- This will give you the following output:


![Show Database](https://user-images.githubusercontent.com/65022146/189537736-f86cea87-2a63-42db-b255-290d28ccaee4.png)



Next, we’ll create a test table named todo_list. From the MySQL console, run the following statement:

   CREATE TABLE example_database.todo_list ( mysql> item_id INT AUTO_INCREMENT, mysql> content VARCHAR(255), mysql> PRIMARY KEY(item_id) mysql> );

- Insert a few rows of content in the test table. You might want to repeat the next command a few times, using different VALUES:

   mysql> INSERT INTO example_database.todo_list (content) VALUES ("My first important item");

- To confirm that the data was successfully saved to your table, run:

    mysql> SELECT * FROM example_database.todo_list;

- After confirming that you have valid data in your test table, you can exit the MySQL console:

   mysql> exit

- Now you can create a PHP script that will connect to MySQL and query for your content. Create a new PHP file in your custom web root directory using your preferred editor. We’ll use vi for that:

  vi /var/www/projectLEMP/todo_list.php

- Paste the text below into the blank file:

TODO
"; foreach($db->query("SELECT content FROM $table") as $row) { echo "
" . $row['content'] . "
"; } echo "
"; } catch (PDOException $e) { print "Error!: " . $e->getMessage() . "
"; die(); }

- Save and close the file when you are done editing.

- Access the browser through the URL below:

    http://<Public_domain_or_IP>/todo_list.php



- You’ll see the following output:



![To do list php](https://user-images.githubusercontent.com/65022146/189538504-02ef55d8-458a-4744-ab34-5ac8321488ee.png)



- That means your PHP environment is ready to connect and interact with your MySQL server.





     


      
         
