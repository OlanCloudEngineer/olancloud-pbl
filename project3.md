A SIMPLE TO DO APPLICATION WITH MERN WEB STACK ON AWS CLOUD

This project shows a step by step process of deploying an application using the MERN Stack.

Pre-requisites:

* An active Virtual Box with Linux(Ubuntu) running on AWS

STEP 1:
Log on to your Virtual Machine using Git Bash

![image](https://user-images.githubusercontent.com/83290893/117485892-d6c6b500-af60-11eb-8791-6b55867a5995.png)

Run the following commands:

sudo apt update
sudo apt upgrade

STEP 2:

Install Node.js on the Virtual Machine using the command below:

sudo apt-get install -y nodejs

Verify the installation using these commands one after another: node -v , npm -v

STEP 3:

Create an application for your project. Here we call our project Todo. From the pwd, run the command below:

mkdir Todo

Navigate to the Todo directory: cd Todo

Run "npm init" command to initialize your project and it create a file called package.json(Keeps the information about your project and its dependencies).

STEP 4:

Install ExpressJS, to do this, remain on the Project(Todo) directory and run the command:

npm install express

Once that is completed. Create a file on the same directory - touch index.js

Install dotenv using the command: npm install dotenv

Next, open the index.js you created earlier - vim index.js

Copy and Paste the code below in the file and save.

![image](https://user-images.githubusercontent.com/83290893/117487419-f959cd80-af62-11eb-960a-a722000c1e1f.png)

NB: You can use your desired port number. Here I used Port 5000.

Before we test our installation, Goto your AWS Dashboard and created an Inbound Security rule to allow traffic on Port 5000.

Next, run the command - node index.js

Output should look like this:

![image](https://user-images.githubusercontent.com/83290893/117487730-5d7c9180-af63-11eb-9d28-d775b2291b51.png)

Finally, open a new browser tab and enter : http://<PublicIP-or-PublicDNS>:5000
  
  Output:
  
  Welcome to Express

STEP 5:

Create your Application. Once, we are done, the application should be able to do the following:

* Create a new task
* Display list of all tasks
* Delete a completed task

To start with, I would create a "routes" folder for each of the task.

Run the command: 

mkdir routes

Change directory to routes folder: cd routes

create a file "api.js" with the command below: touch api.js

Open the file and replace the content with the code below:

![image](https://user-images.githubusercontent.com/83290893/117493929-8b65d400-af6b-11eb-8f07-535e9b10973d.png)

STEP 6:

Create a Model - Goto the Project directory "Todo" and run the command below:

npm install mongoose

Once the installation is completed. Create a new folder with mkdir "models" command

Navigate to the model folder and create a file: touch todo.js

Open "vim todo.js" and update the content of the code with:

![image](https://user-images.githubusercontent.com/83290893/117498503-c965f680-af71-11eb-9b27-90128a7867b8.png)

Open "vim api.js" and update the content of the code with:

![image](https://user-images.githubusercontent.com/83290893/117500130-1ba81700-af74-11eb-987d-8920988738ab.png)

STEP 7:

Setting up MONGO DB

Open a free MongoDB account and select AWS as the Cloud Provider.

![image](https://user-images.githubusercontent.com/83290893/117500672-dafccd80-af74-11eb-9fdd-f05383b9e128.png)

![image](https://user-images.githubusercontent.com/83290893/117500980-52326180-af75-11eb-82dd-7198e9125448.png)


Create a file in your Todo directory and name it ".env" recall that any file with "." shows it is a hidden file. Hence, running ls command would not display the file.

Use this command below:

touch .env
vi .env

Update the content of the file with the Database connection string. In my case:

DB = 'mongodb+srv://OlanDB:Jay11xxxx@olancloud.nyb23.mongodb.net/myFirstDatabase?retryWrites=true&w=majority'

Open the vim index.js file and update the content with the code below:

![image](https://user-images.githubusercontent.com/83290893/117507803-772bd200-af7f-11eb-8d0f-abbf140bf689.png)
![image](https://user-images.githubusercontent.com/83290893/117507831-83b02a80-af7f-11eb-87f5-0c985e828284.png)

Next you can start the server with the command: node index.js

![image](https://user-images.githubusercontent.com/83290893/117507943-afcbab80-af7f-11eb-924f-80fde32e2ec4.png)

STEP 8:

Testing the Backend Code 

Install Postman. You can download and use the free version.

create a POST request to the API - http://3.23.129.129:5000/api/todos
Add Content-Type - application/json

create a GET request to the API - http://3.23.129.129:5000/api/todos

create a DELETE request to the API - http://3.23.129.129:5000/api/todos

STEP 9:

Creation of the FrontEnd

On you Project(Todo) directory, run the following commands:

 npx create-react-app client
 
 npm install concurrently --save-dev
 
 npm install nodemon --save-dev

Next, open the package.json file in the pwd and update the block content of the file as shown below:

![image](https://user-images.githubusercontent.com/83290893/117508739-fcfc4d00-af80-11eb-9f0c-a49d0c80bbda.png)

Configure the package.json file as shown below:

Change the Directory - cd client

Open the file and update the content - vi package.json

Add the line below:

"proxy": "http://localhost:5000"

To open and start running the application server use: npm run dev

You will observe the application is now running on port 3000. Hence, you need to create an inbound rule to allow the application to be accessed externally.

STEP 10:

Creation of the REACT Component. Start by running the following commands:

cd src

mkdir components

cd components

touch Input.js ListTodo.js Todo.js

vi Input.js

Update the content of the file with the code below:

![image](https://user-images.githubusercontent.com/83290893/117509610-734d7f00-af82-11eb-829e-a0835a57f468.png)
![image](https://user-images.githubusercontent.com/83290893/117509638-806a6e00-af82-11eb-9d2b-6f99a2e7d532.png)

Once, that is completed. navigate to the src folder.

Run: npm install axios - To install the Axios

cd src/components

vi ListTodo.js - Update the content of the file with the code below:

![image](https://user-images.githubusercontent.com/83290893/117509863-e35c0500-af82-11eb-9b3d-d3f802724a63.png)

vi Todo.js -  Update the content of the file with the code below:

![image](https://user-images.githubusercontent.com/83290893/117509970-1d2d0b80-af83-11eb-8898-292c994689df.png)
![image](https://user-images.githubusercontent.com/83290893/117510032-3a61da00-af83-11eb-8d11-1db4a235bd85.png)

Next, run the commmand below:

cd ..
vi App.js -  Update the content of the file with the code below:
![image](https://user-images.githubusercontent.com/83290893/117510193-8c0a6480-af83-11eb-983e-0cc10b70a717.png)

vi App.css -  Update the content of the file with the code below:
![image](https://user-images.githubusercontent.com/83290893/117510379-e1df0c80-af83-11eb-97fa-46e738594ce7.png)
![image](https://user-images.githubusercontent.com/83290893/117510414-f1f6ec00-af83-11eb-8dc0-d995f399e022.png)
![image](https://user-images.githubusercontent.com/83290893/117510477-0a670680-af84-11eb-97d7-ca31903d7983.png)

vim index.css - Update the content of the file with the code below:
![image](https://user-images.githubusercontent.com/83290893/117510551-2ec2e300-af84-11eb-9cca-645bf17a7ad7.png)

Finally, run this command from the Todo Project Directory: npm run dev

Output:
![image](https://user-images.githubusercontent.com/83290893/117510753-85302180-af84-11eb-8c7b-087ef00396cd.png)


















