---
title: "Part-2 | Deploying a 2-Tier Application in EKS using Helm."
seoTitle: "Part-2 | Deploying a 2-Tier Application in EKS using Helm."
seoDescription: "Part 2 of our DevOps blog series: Containerizing applications and databases on AWS, step by step."
datePublished: Thu Oct 19 2023 05:43:17 GMT+0000 (Coordinated Universal Time)
cuid: clnwrai8000020ala05nx4cx5
slug: part-2-deploying-a-2-tier-application-in-eks-using-helm
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697056714338/0592c7dd-2cb5-48d8-987e-843e4c7614c3.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1697694102318/610e93bf-765d-4008-beaf-5d6066de6fcd.png
tags: docker, mysql, kubernetes, devops, cicd-cjy1vtdk2005kjjs17n8couc3

---

Hello learners,

I'm back with **Part 2** of the current Series.

First of all, my sincere thanks and gratitude to Shubham bhaiyaa (TrainwithShubham) for releasing this series. I'm going to document the process for you guys.

### Overview:

In this Part, we are going to create Dockerfile for our application and database and push the image to Dockerhub. For this, first of all, we need a server.

This project we will be doing on AWS Cloud, so let's create an EC2 instance.

### Step 1: Create an EC2 instance and Install Docker

I hope as you all have come a long way, you already know how to create an EC2. If you don't know, just explore. It's very easy.

Here is our EC2 of t2.micro and running Ubuntu OS.

> **Make sure, HTTP, HTTPS, and other required ports are open in the security group.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697058139868/6039bfd7-7c07-4c2a-9633-c9865a33890f.png align="center")

We will install docker here.

```bash
sudo apt-get update
sudo apt-get install docker.io -y
sudo apt-get install docker-compose -y
```

Now give permission to current user for docker service so that we can run docker command without sudo.

```bash
sudo chown $USER /var/run/docker.sock
```

### Step -2: Clone Source Code

Now it's time to clone our code here, and then move to the project directory.

```bash
git clone https://github.com/sitchatt/two-tier-flask-app.git
cd two-tier-flask-app/
```

Please Note, that if you now do "ls" command here, you may see **Dockerfile** already present. The best way to learn is to delete the Dockerfile with **"rm Dockerfile"** command and write on your own.

### Step 3: Creating a Docker network

Now, We need something that can help to create a bridge between the app container and the db container so that can be connected. Here Docker Network comes into the picture.

Let's create a Docker Network.

```bash
docker network create twotierapp
```

### Step 4: Building Containers

Now, that we have the Dockerfile, let's build an image from there and eventually create a container. Also as we have a DB to connect, we need to add the app container to the network and also we need to pass few environment variables.

```bash
docker build -t flaskapp:latest .
docker run -d -p 5000:5000 --network=twotierapp -e MYSQL_HOST=mysql -e MYSQL_USER=root -e MYSQL_PASSWORD=admin -e MYSQL_DB=mydb --name=flaskapp flaskapp:latest
```

Create the mysql container now.

```bash
docker run -d --name mysql  --network=twotierapp -e MYSQL_DATABASE=mydb  -e MYSQL_ROOT_PASSWORD="admin" -p 3306:3306 mysql:5.7
```

> **Explanation**: This command will run the docker container in detach mode. **3306** is the port where MySQL runs by default. For any DB, we need to provide some environment variable. Here we need to provide the ROOT password in advance to perform the operation later on. Lastly, we need to specify which MySQL version we will be using here. So we are using MySQL 5.7 here.

Now if you run "**docker ps**" command, you can see the containers are running.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697484839622/4c8962c9-c925-4fb2-9508-19ed77e63665.png align="center")

Now, if you will check, our application is up and running in port **5000.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697484890856/adc9014e-b657-40a6-b89b-6d19648fdff1.png align="center")

Oh!!! We got an Error !!! 😬

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697484920641/5a77365a-a771-4ce8-b33c-5a7db9f11f80.gif align="center")

Wait! Don't Quit! As a DevOps Engineer, you need to understand the error and look for the solution. The best way to do it, is to read the error message itself. Here is the error message showing that we need a MySQL table to store the data, which eventually may resolve this error.

Let's try it Out!

### Step 5 : Creating MySql Table

For that, we need to **log in** inside the MySQL container and create a table there.

Run this command and login to your container.

```bash
docker exec -it <your container id> bash
```

Now after logging in to the container, switch to root and run the below command to create a table.

```bash
mysql -u root -p
```

Now we need to use the mydb database to create a table.

```bash
show databases;
use mydb;
CREATE TABLE messages ( id INT AUTO_INCREMENT PRIMARY KEY, message TEXT );
```

Snippet for reference:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697485784141/83db687d-c05e-4594-9316-c7085e0b269f.png align="center")

> **⚠️ Imp Note: please do check the database's exact name with the show databases command because there might be a change concerning capital and small letters. You might need to update your docker-compose file accordingly.**

And now BOOM !! 🚀

We can see our application is running. Just test if it's working well and storing the data in the database.

1. Writing is working in application:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697485922861/3270d94c-3e43-4481-9f8f-36f9dc42ddb5.png align="center")

1. Input is being stored in MySql DB.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697486020991/98e47935-3167-440b-9941-70272c407c24.png align="center")
    

Exit from the container now.

In the Next blog, we will see how we can manage the containers via **Docker-compose.**

Stay Tuned!!!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697486150341/2d2616e1-592a-4416-a0c8-f3e4e2cc0da9.gif align="center")

💖 Thanks for being with me till the end. I hope that I provided you with some useful knowledge. Don't forget to spread the blog to your friends and community. 💖

Feel free to ask any questions, I'm just a DM away.👍

### Follow *Sitabja Chatterjee* for more content! ✌️