---
title: "Part-3 |  Deploying a 2-Tier Application in EKS using Helm."
seoTitle: "Part-3 |  Deploying a 2-Tier Application in EKS using Helm"
seoDescription: "Master Docker container management with Docker Compose on our Hashnode blog. Learn the art of efficient container operation. #DockerCompose #ContainerManage"
datePublished: Mon Oct 30 2023 13:28:30 GMT+0000 (Coordinated Universal Time)
cuid: clocxr5yv001009id7nlb4zko
slug: part-3-deploying-a-2-tier-application-in-eks-using-helm
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697486384590/7c222a3f-03d4-4fca-aa67-b7dc79071935.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1698672342564/c69a5707-427e-4acb-87e5-03723bbd335f.png
tags: docker, kubernetes, devops, eks, ci-cd

---

Hello learners,

I'm back with **Part 3** of the current Series.

First of all, my sincere thanks and gratitude to Shubham bhaiyaa (TrainwithShubham) for releasing this series. I'm going to document the process for you guys.

### Overview:

In this Part, we are going to manage our docker containers with Docker-compose which is an easier and more automated way to operate docker containers.

We already have **docker-compose.yml** file in our code. You can use that or can create your own.

### Step 1: Log in to Dockerhub and push the existing images

You can use below command to perform that.

```bash
docker login
```

Tag the image with the dockerhub username so that dockerhub can recognize that.

```bash
docker tag flaskapp:latest <docker username>/flaskapp:latest
```

Now Push the image to docker hub.

```bash
docker push <docker username>/flaskapp:latest
```

It will now reflect on your docker hub.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697487663023/6b0a97b0-0685-4ae3-8177-a82cd83eb7b7.png align="center")

### Step 2 : Create Docker-compose file

Now create a docker-compose.yml file with your image or you can use the existing one.

Note: If you don't have an docker image and want to build the image first, you should add these lines in your code.

```bash
backend:
  build:
    context: .
```

We already have an image so we are using the below.

```bash
version: '3'
services:
  backend:
    image: sitabjadocker/flaskapp:latest
    ports:
      - "5000:5000"
    environment:
      MYSQL_HOST: mysql
      MYSQL_USER: admin
      MYSQL_PASSWORD: admin
      MYSQL_DB: mydb

    depends_on:
      - mysql

  mysql:
    image: mysql:5.7
    ports: "3306:3306"
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: mydb
      MYSQL_USER: admin
      MYSQL_PASSWORD: admin

    volumes:
      - ./message.sql:/docker-entrypoint-initdb.d/message.sql   # Mount sql script into container's /docker-entrypoint-initdb.d directory to get table automatically created
      - mysql-data:/var/lib/mysql  # Mount the volume for MySQL data storage

volumes:
  mysql-data:
version: '3'
services:
  backend:
    image: <your docker id/image name:tag>
    ports:
      - "5000:5000"
    environment:
      MYSQL_HOST: mysql
      MYSQL_USER: admin
      MYSQL_PASSWORD: admin
      MYSQL_DB: mydb

    depends_on:
      - mysql

  mysql:
    image: mysql:5.7
    ports: 
      - "3306:3306"
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: mydb
      MYSQL_USER: admin
      MYSQL_PASSWORD: admin

    volumes:
      - ./message.sql:/docker-entrypoint-initdb.d/message.sql   # Mount sql script into container's /docker-entrypoint-initdb.d directory to get table automatically created
      - mysql-data:/var/lib/mysql  # Mount the volume for MySQL data storage

volumes:
  mysql-data:
```

### Step 3: Run Docker Compose Up

Now stop and remove running containers to give it a fresh start.

To start using docker-compose, run the command

```bash
docker-compose up -d
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697494165397/e852cc78-dfe4-49fc-9734-b5b82d0b7c7c.png align="center")

### Step 4: Test Application:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697494191611/3f9c6f0a-0dcb-4553-a359-cbe260793d6b.png align="center")

And now BOOM !! 🚀

We can see our application is running.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697494350512/cb0bcca3-4483-499c-b25e-d953e7bd6715.gif align="center")

💖 Thanks for being with me till the end. I hope that I provided you with some useful knowledge. Don't forget to spread the blog to your friends and community. 💖

Feel free to ask any questions, I'm just a DM away.👍

### Follow *Sitabja Chatterjee* for more content! ✌️