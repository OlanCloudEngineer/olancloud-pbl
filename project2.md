DEPLOYING WEB SOLUTION USING LEMP STACK

This project explains steps for implementing LEMP stack on AWS Cloud Environment.

It is assumed that you have an existing AWS Subscription and have setup your Linux O/S on your Virtual Box. If not, you can open a Free Tier account.

Step 1: Installing NGINX Webserver and Updating Firewall
To install Nginx, connect to the Cloud Virtual Machine using Git Bash. Once you are in the Virtual Machine. Run the command below:

<sudo apt update>
  
<sudo apt install nginx>
  
Once the installation is complete. You can run the following command to confirm NGINX was installed properly.

<sudo systemctl status nginx>

Once you have installed the Web server properly. You can run the command below:

curl http://localhost:80 on the Git Bash window or open a new browser and enter the public address IP i.e http://<Public_ip_address>

![image](https://user-images.githubusercontent.com/83290893/117007173-3adb4600-ace1-11eb-9a2b-a99e9dc59fd2.png)

Step 2: Installing MySQL

After the website has successfully be hosted, your website needs to talk to a Database. In this project, we are using MySQL. Let's get into action immediately.

Again, use ‘apt’ to acquire and install this software:

<sudo apt install mysql-server>
  
 Once, the command runs successfully, you can see the percentage progress on the terminal window until its completion. During the installation, you will be prompted to confirm installation. Press Y to continue.
 
 After the installation is completed. You can run the command below to add a layer of security to the Database. sudo mysql_secure_installation
 
 It will ask you to configure your password. Add the password using a mixture of Upper and Lower case Letters with Numbers and Special characters. What this does is to give your DBMS a higher level of security.

Once, you are done. You can test what you have done using the command below: sudo mysql

![image](https://user-images.githubusercontent.com/83290893/117008156-5561ef00-ace2-11eb-976f-774aada839db.png)

If your setup was fine, you should get the screen above. To exit the environment use the command below: mysql> exit

Step 4: Installing PHP

Now that you have install the NGINX for hosting the website, the MySQL as the relational database to store your data. You need to setup PHP to handle dynamic content displayed to the Users.

2 packages are required to be installed. To do this, run the following command: <sudo apt install php-fpm php-mysql>

Once the installation is completed, you can run the following command to confirm your PHP version: <php -v>

Your output should look like this:

![image](https://user-images.githubusercontent.com/83290893/117008882-141e0f00-ace3-11eb-859a-d8b8a100b273.png)

Step 4: Configuring NGINX to use PHP Processor

Nginx has one server block enabled by default and is configured to serve documents out of a directory at </var/www/html>. So you can create another folder in the directory since we considering hosting multiple websites on a single machine.

Let's create the root web directory for a new domain as follows:

<sudo mkdir /var/www/projectLEMP>

To assign neccessary priviledge to the current user. Run the following command:

<sudo chown -R $USER:$USER /var/www/projectLEMP>

Now, you can create a new file called projectLEMP in the path below:

<sudo nano /etc/nginx/sites-available/projectLEMP>

Enter the sample code below and save the file using CNTL + X. Then press Y to save.

<
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
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
     }

    location ~ /\.ht {
        deny all;
    }

}
>
Activate your configuration by linking to the config file from Nginx’s sites-enabled directory using the command below:

<sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/>

Next, to confirm all configuration has been OK so far, run the command below:

<sudo nginx -t>

To  disable default Nginx host that is currently configured to listen on port 80, run this command:
  
  







