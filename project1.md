 **DEPLOYING WEB SOLUTION USING LAMP STACK**
``
This project explains steps for implementing LAMP stack on AWS and Azure Cloud Environment.

It is assumed that you have an existing Microsoft Azure Subscription or AWS Subscription. If not, you can open a Free Tier account on both platforms.

**Step 1: Installing Apache and Updating Firewall**
 
To install Apache, connect to the Cloud Virtual Machine using Terminal Window or Putty. Once you are in the Virtual Machine. Run the command below:

`sudo apt update` - The command ensures that all necessary files are up to update on the Virtual machine.
`sudo apt install apache2` - To install the apache setup

To verify that apache2 is running as a Service in on the Linux Virtual Machine OS, use following command
`sudo systemctl status apache2`

![image](https://user-images.githubusercontent.com/83290893/116623161-b9309480-a93d-11eb-96d4-af64dec93bfe.png)

The green "active(running)" shows that the Apache was successfully installed.

At this point, the webserver has been successfully launched. Yipee!!!

Next, you need to permit inbound traffic reaching the Webserver to access your webpages on Http(Port 80). Navigate to your Cloud Management Portal (AWS or Azure). 

Click on the security Group, then Inbound rules. Add a new rule to allow inbound traffic on Port 80.

**AWS - Virtual Machine**
![image](https://user-images.githubusercontent.com/83290893/116623848-cdc15c80-a93e-11eb-99fa-11ab9c6aa5db.png)
 
**Azure - Virtual Machine**
![image](https://user-images.githubusercontent.com/83290893/116624193-67890980-a93f-11eb-9705-7e0f132fe0eb.png)

To confirm the rule was set correctly, Run the command below on your terminal window

`curl http://localhost:80`

It should display an html webpage as shown below:

![image](https://user-images.githubusercontent.com/83290893/116624485-e3835180-a93f-11eb-965d-18680a4f948a.png)

Alternatively, you can launch a web browser on your Host Machine as run the command below:

`http://<Public-IP-Address>:80` - Note: your public IP address can be found on the Cloud Management Portal

If it opens a standard web page. It means your have successfully launched a Website on Cloud infrastructure. Bravo!!!

**Step 2: Installing MySQL**

After the website has successfully be hosted, your website needs to talk to a Database. In this project, we are using MySQL. Let's get into action immediately.

Again, use ‘apt’ to acquire and install this software:

`sudo apt install mysql-server`

Once, the command runs successfully, you can see the percentage progress on the terminal window until its completion. During the installation, you will be prompted to confirm installation. Press Y to continue.

After the installation is completed. You can run the command below to add a layer of security to the Database.
`sudo mysql_secure_installation`

It will ask you to configure your password. Add the password using a mixture of Upper and Lower case Letters with Numbers and Special characters. What this does is to give your DBMS a higher level of security.

Once, you are done. You can test what you have done using the command below:
`sudo mysql`

![image](https://user-images.githubusercontent.com/83290893/116625602-d4050800-a941-11eb-9902-19ee64e6c9aa.png)

If your setup was fine, you should get the screen above. To exit the environment use the command below:
`mysql> exit`

**Step 3: Installing PHP**

Now that you have install the Apache for hosting the website, the MySQL as the relational database to store your data. You  need to setup PHP to handle dynamic content displayed to the Users.

3 packages are required to be installed. To do this, run the following command:
`sudo apt install php libapache2-mod-php php-mysql`

Once the installation is completed, you can run the following command to confirm your PHP version:
`php -v`

Your output should look like this:

![image](https://user-images.githubusercontent.com/83290893/116626484-33afe300-a943-11eb-8909-7d7e10769d0c.png)

At this point, your LAMP stack is completely installed and fully operational. Great Stuff!!!

- Linux OS
- Apache HTTP Server
- MySQL
- PHP

**Step 4: Create a Virtual Host for your Website using Apache**
The essence of setting up a Virtual Host is that it allows you to host more than one website on the same machine. So in this stage, you can decide to specify the name to give to your second website. For me I name it _projectlamp_.

Create the directory for projectlamp using ‘mkdir’ command as follows:
`sudo mkdir /var/www/projectlamp`

Due to the priviledges required to alter the www folder on the Linux Machine. You need to assign sufficient right to the current system user by running this command:
`sudo chown -R $USER:$USER /var/www/projectlamp`

Create and open a new configuration file in Apache’s sites-available directory using your preferred command-line editor. You can 





