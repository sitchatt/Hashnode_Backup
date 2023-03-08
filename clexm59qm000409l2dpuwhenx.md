---
title: "Multi-Stage Docker file"
seoTitle: "Creating Minimal and Secure Docker Images with Multi-Stage Dockerfile"
seoDescription: "Learn how to create small and secure Docker images using multi-stage Dockerfiles and Distroless images."
datePublished: Tue Mar 07 2023 02:09:39 GMT+0000 (Coordinated Universal Time)
cuid: clexm59qm000409l2dpuwhenx
slug: multi-stage-docker-file
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1678130491405/fcf81028-e45f-4e93-8bfe-9f550d765a13.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1678131761698/6d0793e3-16c0-4996-9f92-e2df173539ed.jpeg
tags: docker, devops, docker-images, multi-stage-docker-file, distroless-image

---

Hey learners,

Today I'm bringing a very demanding and important topic to everyone so that everyone can get to know how to **reduce the size** of Docker-image significantly and also increase the **security of Docker containers**.

So, let's learn!

At the end of the blog, I'll add a few additional links, so that you can check those out later.

For those who don't know what is Docker image, let's understand that first in-short.

# What is Docker and Docker image?

**Ans**: Docker is a containerization platform that allows developers to create, deploy, and run applications in a container, which is a lightweight, portable environment.

A Docker image is a template that contains the programme code, dependencies, and runtime environment required to run a particular application. Every system that supports the Docker platform can run Docker containers because they are created and launched using Docker images. Docker images can be kept in registries like Docker Hub, Nexus, ECR etc. where other developers can quickly download and share them.

Now let's see, what is ***multi-stage*** docker image is in short.

# What is a Multi-stage Docker image?

**Ans:** Dockerfiles with multiple stages are an excellent way to create smaller and more efficient Docker images. You can separate the build process from the runtime environment by using multiple stages in a Dockerfile, resulting in a smaller image size that only includes the dependencies and libraries required to run your application.

You can have **"n"** number of stages in your multi-stage docker file.

In multi-stage, the **build stages** of Dockefile size, will not be added to your docker image, only the **entry-point section(last stage)**, where we pass certain commands to **run** our application with a specific runtime.

Before seeing the magical difference of a multi-stage docker file, let's also learn one of the new terms called ***"distroless image" . ;)***

# What is Distroless Image?

**Ans:** Distroless is a Docker image that is published by Google, and **does not include any operating system** packages or utilities. These images contain only the dependencies needed to run a specific application, such as **runtime** libraries and the application **binary** itself. Distroless images are frequently used in containerized environments to **improve security** and reduce the application's attack surface.

It allows you to eliminate the OS in the containers to the bare minimum application that needs to run. Basically It will package only `application + dependencies` in a container image.

A Linux distro is made up of two main components: **a kernel,** and a **user space**. Remember, a distroless image must always run on a kernel.

Now, here the wait is over! :).

Let's see what is the ;

# Impact of multi-stage with distroless image over a normal Dockerfile.

We are taking an example application made on go-lang. I've chosen golang application as go-lang doesn't require even a run server to run, thus we can understand the ultimate compression of docker image.

All the links I'll be added at the end of the blog as well as a LinkedIn post with credits.

## Steps:

1. First of all, clone my GitHub repo in your machine:
    

```bash
sudo apt-get update && sudo apt install git
```

```bash
git clone https://github.com/sitchatt/go-lang-calculator.git
```

1. Now install go-lang to test the application:
    
    ```bash
    sudo apt install golang-go
    ```
    
2. Move to the application folder and run the application and see if it's working:
    
    ```bash
    go run calculator.go
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678122230430/2ef4368b-6114-4fc4-b222-fca55627a005.png align="center")
    
    Now, it's time to make the Dockerfile.
    
3. Below is an example of the Dockerfile. You can either copy or try it yourself too.
    
    ```bash
    ###########################################
    BASE IMAGE
    
    ###########################################
    
    FROM ubuntu
    
    RUN apt-get update && apt install golang-go
    
    ENV GO111MODULE=off
    
    COPY . .
    
    RUN CGO_ENABLED=0 go build -o /app .
    
    ENTRYPOINT ["/app"]
    ```
    
4. Now Build the docker image
    
    ```bash
    docker build -t <tag> .
    ```
    
5. If you check the docker images data :
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678126905864/0a0fa59c-f922-4a9d-bc68-02f43a820f59.png align="center")
    
    As you can see, the image size is **862 MB** .
    

Now, let's see ;

### Steps to Run Multi-stage docker file:

Now let's try writing the multi-stage docker file.

We will also use **"scratch"** as a *distroless* image used for **go-lang.**

***Note: You can choose distroless images for any programming language such as python or java etc from this*** [*Official GitHub Link*](https://github.com/GoogleContainerTools/distroless) *.*

Let's see the multi-stage docker-file first and I'll try to explain it in short later.

```bash
###########################################
BASE IMAGE

###########################################

FROM ubuntu AS build

RUN apt-get update && apt-get install -y golang-go

ENV GO111MODULE=off

COPY . .

RUN CGO_ENABLED=0 go build -o /app .

############################################

HERE STARTS THE MAGIC OF MULTI STAGE BUILD

############################################

FROM scratch

# Copy the compiled binary from the build stage

COPY --from=build /app /app

# Set the entrypoint for the container to run the binary

ENTRYPOINT ["/app"]
```

**Explanation:**

In this multi-stage Dockerfile, we again use ubuntu as base image to build the Go application and also added Alias **"AS build"** , as we need to **'call'** it later. You can give any name as alias.

However, in the final image, we use the `scratch` image, which is a minimal image for go-lang that includes only the necessary runtime libraries. Now , we have copied the application binary from the previous build, and run the application through ENTRYPOINT.

This creates a smaller, more secure Docker image that only contains the necessary components to run the Go application, as the final run happened upon "**scratch**" and the previous build phase data will be excluded here. Only the compiled binary, which is very less size, will be used in new phase.

Now, if you build the docker image from this `Dockerfile` , you can see the image size as low as **1.83 MB.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678129233730/67a16ea1-14bd-42e6-9df0-6804b899032e.png align="center")

You can push this image to DockerHub or Nexus etc and use it to build a container with this.

Thank you so much for reading till last! Hope you have gained some fruitful knowledge from it. Don't forget to share it with your community and friends.

If you have any more questions or need further assistance, feel free to ask.

# Some Useful Links:

1. [Project Inspiration](https://youtu.be/yyJrZgoNal0)
    
2. [Source Code](https://github.com/sitchatt/go-lang-calculator.git)
    
3. [How to push/pull image from DockerHub](https://medium.com/@sitabjachatterjee158/how-to-push-pull-image-in-docker-hub-c7377015337e)
    
4. [Docker Basics](https://rushikesh-mashidkar.hashnode.dev/what-is-docker-get-started-with-docker)
    
5. [Advanced Docker-concepts](https://rushikesh-mashidkar.hashnode.dev/dockerfile-docker-compose-swarm-and-volumes)
    
6. [Multi-Stage Docker file Official Document](https://docs.docker.com/build/building/multi-stage/)