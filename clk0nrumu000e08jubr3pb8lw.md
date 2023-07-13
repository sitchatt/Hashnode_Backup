---
title: "Architect and Build an End-to-End  Web Application from Scratch using AWS Amplify"
seoTitle: "AWS Amplify: Simplify App Development with AWS Services"
seoDescription: "Explore AWS Amplify: Build scalable web and mobile apps with ease using Lambda, API Gateway, DynamoDB, and IAM integration. Simplify development."
datePublished: Thu Jul 13 2023 04:37:03 GMT+0000 (Coordinated Universal Time)
cuid: clk0nrumu000e08jubr3pb8lw
slug: architect-and-build-an-end-to-end-web-application-from-scratch-using-aws-amplify
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1689204810274/03f09601-dc71-4a05-bb5c-76910e5cb97f.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1689222832671/37699413-72f5-48dc-9192-bcc133bfd413.jpeg
tags: dynamodb, rest-api, api-gateway, awsamplify, awsamplifyhackathon

---

Hello Learners,

Welcome to **5th blog** on my series of **#Exploring\_AWS\_Services.**

Just got to know that AWS, in association with Hashnode, is conducting a program called "AWS Amplify Hackathon". Check the details [Here](https://hashnode.com/hackathons/aws-amplify-2023?source=hackathon-feed-widget).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689221719939/257b003a-3382-4c83-a364-940af2d17276.png align="center")

So, I became curious about the service and started exploring. And till I understood the advantages, I became a fan of this service. It's having amazing features such as easiest app deployment, by default dockerized along with CD integrated via SCM webhook.

In this blog, I will introduce to you guys another AWS Service called **"AWS Amplify" 🎉**

Though, we will be using other various AWS services across the project.

Let me quickly introduce you to those.

> 🎯 AWS Services Used in this Project:
> 
> ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689206273358/dc7582f2-69f0-480b-820f-51639622b400.png align="center")
> 
> 1. **AWS Amplify:** AWS Amplify is a development platform that offers a complete collection of tools and services for developing scalable and secure web and mobile applications. It facilitates development by providing capabilities like authentication, storage, and API management.
>     
> 2. **AWS Lambda:** AWS Lambda is a serverless computing solution that allows you to run code without the need for server provisioning or management. It scales your applications automatically in response to incoming requests and executes your code in reaction to various events, such as data changes or
>     
>     user activities.
>     
> 3. **API Gateway:** AWS API Gateway is a fully managed service that simplifies the creation, publication, and management of APIs at any scale. It serves as a portal via which applications can access data, business logic, or functionality from backend services such as Lambda functions or EC2 instances.
>     
> 4. **DynamoDB**: AWS's DynamoDB is a fast and flexible NoSQL database service. It is intended to deliver low-latency performance at any scale, making it appropriate for applications requiring high availability and scalability. For durability, DynamoDB stores data in key-value pairs and automatically replicates it across various availability zones.
>     
> 5. **AWS IAM :** AWS Identity and Access Management (IAM) is a service that allows you to regulate access to AWS services in a secure manner. IAM enables you to manage users, groups, and roles, as well as set fine-grained permissions to regulate who has access to which resources and can execute specified actions within your AWS account.
>     

Now let's move toward our project setup.

# Step-1: Have one "index.html" file

To build your web app, the first thing you need is an **index.html** file.

I've stored my index.html file in my [GitHub Repo](https://github.com/sitchatt/Build_WebApp_Using_AwsAmplify/blob/main/index.html). You can use any code of your choice.

# Step -2: Configure AWS Amplify to host our web app

For this, Go to the AWS Amplify page &gt; Scroll down &gt; Click on "**Host your web app**".

Now, you should see a screen asking you to provide the source of the code. You can give anything as per you, even the "*Deploy without git provider*" option too if you saved locally only. As I've saved in my GitHub, I'll use the "***GitHub"*** option.

Click on '**Continue**'.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689207844487/d27972aa-2021-416e-a70a-c313c52652be.png align="center")

It will then ask you to authorize and install it. Do the same.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689208039848/3f491e1f-c3ee-4f44-ab67-aded1b73222d.png align="center")

Then, it will ask you to add the Repository and Branch. Add yours and click on "Next".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689208271986/dc758512-f0eb-4464-b1c5-d1c2d261e130.png align="center")

Give your app a name according to you. Also, for this project, tick on to allow *Amplify to automatically deploy all*, as we have only one for our case.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689208606274/90f2b932-44d7-45dd-9b2f-0e6e3f418878.png align="center")

Then simply **"Save & Deploy".**

You could see, the build process is already started . Isn't it amazing to see our app is deploying with just a few mouse clicks only? 😍

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689208856175/9a73d288-28f6-48a7-bf9f-1fb1d00e4303.png align="center")

( It will take ~15 mins to deploy fully)

If you click on the build flow section, you can see the detailed view of this. You can see, which docker engine is provisioning, also you can see the Dockerfile and other logs.

Just expand the options and explore.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689209602098/98e016ab-8e86-4bf6-b23d-67e8d00cb84b.png align="center")

If you click on the domain link, shown in the above screenshot, it will redirect you to the newly built web app. And It's Runninggggg!! 🤩

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689209997643/ee78d014-784c-4603-a065-9253286597a0.png align="center")

# Step-3: Create a Lambda Function to calculate the mathematics

So, after our web app is deployed, our motto is to use that to calculate the power of our input.

For that, we need a code. And to run the code, we will use lambda function, as you know *lambda function runs in response to some trigger*.

We will use Python code for this. So we will create a lambda function with **Python 3.10.**

As you are following this series, you should already know how to create a lambda function. I'm sharing the steps here again for someone new, for detailed screenshots, kindly check out my previous blogs.

Search for `lambda` &gt; Click on `Create function` &gt; Provide your desired name and choose runtime as `Python 3.10` &gt; `Create function`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689211396426/ecb584ce-3e96-4d86-b03a-16296bde1557.png align="center")

Now, we need to change to default code to functioning code. Then we need to **Deploy** the code in order to make the lambda function work accordingly.

```bash
# import the JSON utility package
import json
# import the Python math library
import math

# define the handler function that the Lambda service will use an entry point
def lambda_handler(event, context):

# extract the two numbers from the Lambda service's event object
    mathResult = math.pow(int(event['base']), int(event['exponent']))

    # return a properly formatted JSON object
    return {
    'statusCode': 200,
    'body': json.dumps('Your result is ' + str(mathResult))
    }
```

If you are facing an issue copying from here, check out the file [HERE](https://github.com/sitchatt/Build_WebApp_Using_AwsAmplify/blob/main/lambda_functio_without_db).

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689211912756/0bd91c10-a039-4ee0-b491-03d0e50dfcfe.png align="center")

You can test the function also to cross-verify. I've done it and it passed successfully.

You can try as shown below.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689212798407/b88901b7-7015-4d49-8d36-e442b3580e22.png align="center")

**Output:-** Status code should be **200 ,** as you can see, we are getting the answer also.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689212975512/b0896536-5986-45f7-878c-a8ac681526f7.png align="center")

# Step-4: Create a REST API

As of now, we have our web app and also one lambda function to handle the calculation part. Now, as we did trigger manually just now, our users aren't going to log in to the AWS console and trigger the event manually, right? This is not at all a realistic approach.

So, to invoke the lambda function, we need a public endpoint or URL, that can be called to trigger the function.

For this, we will be using the **AWS** **API gateway** to create a **REST API.**

So, navigate to the API gateway console &gt; Build a REST API.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689213607035/a2255df6-8585-4dc7-b61e-63cd82193b3f.png align="center")

Choose Protocol as **REST**, and in the next section, choose **New API**, Provide any **name** and then click on **Create API**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689213758862/15a815c3-3320-4c5c-8736-249349fd58d7.png align="center")

Now, click on "**Resources**" , Make sure "**/**" is selected, drop down and click on "**Create Method**"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689214095492/dcb3f9a9-692a-4e97-873f-717c88460e0c.png align="center")

Now , we will select our Method as "**POST**" as users are going to send data as input.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689214076240/2bdf1e35-da83-4569-be32-903de964ab4f.png align="center")

Click on the ✔️(tick) icon beside "POST" dropdown.

Fill that as shown below and click on "Save". Click on "OK" if any pop-up appears.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689214581100/29a1771b-8050-42de-b4d7-43145e0ca331.png align="center")

Now again, drop down the Actions, and click on **"Enable CROS".**

facilitating CORS (Cross-Origin Resource exchange) in a REST API allows client-side web applications from various domains to access resources, facilitating cross-domain data exchange while ensuring security.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689214733470/a6f784d9-dedf-439b-aa5e-1bfb11837eaa.png align="center")

Now, click on Enable CROS (red mark) and Replace the existing value.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689214921991/c76c2fc4-a080-458f-81df-2a42fecbf6da.png align="center")

Then, Deploy the API with deployment stage on your wish such as dev, prod etc.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689215064249/30ed9a5b-3e4e-4b7d-bee0-700b755d31e5.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689215117671/2e14052b-8c98-4fe6-afe2-6891f2077df6.png align="center")

**Note: Save the invoke URL link for furture purpose.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689215215994/7d72ff50-7748-49e3-bcf1-eccbea44a4a0.png align="center")

# Step-5 : Setting Up DynamoDB Database for storing data

Search for Dynamo DB in AWS console.

1. Click on **create table** on the overview page.
    
2. Give the database name and in Partition Key section, type "**ID**" and create table keeping rest as default.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689215851038/32e48f36-a997-4a0c-a580-4b079692c4bb.png align="center")
    
    1. Navigate to the database , in General Information, expand the Additional Info and copy the **ARN** and save locally for future use.
        
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689216111853/dd71f77a-62b7-48a2-aa0e-ba6c414cfa1f.png align="center")
    
    # Step-6: Giving Permission to Lambda to write to the DynamoDB
    
    Head towards the function &gt; click on configuration &gt; Permission &gt; Click on Role Name.
    

On the new window, on the permission policy section, click on "*Create Inline Policy*"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689216794603/7817e8f2-7bef-424f-a56e-74140a8c1d64.png align="center")

Change the policy

```json
{
"Version": "2012-10-17",
"Statement": [
    {
        "Sid": "VisualEditor0",
        "Effect": "Allow",
        "Action": [
            "dynamodb:PutItem",
            "dynamodb:DeleteItem",
            "dynamodb:GetItem",
            "dynamodb:Scan",
            "dynamodb:Query",
            "dynamodb:UpdateItem"
        ],
        "Resource": "YOUR-TABLE-ARN"
    }
    ]
}
```

**<mark>Note: Make sure you add your saved ARN here before implementing.</mark>**

Click on Next, Give a name, and Create Policy.

# Step -7: Modify Lambda Function code

Hey, did you have one glass of water? I know you are sitting ideal for soo long and now it's time to have some water.

You have the water, meanwhile, let me share you with the updated lambda function code which now can able to handle DynamoDB as well.

Change the lambda code as mentioned and Deploy. You will find the code [HERE](https://github.com/sitchatt/Build_WebApp_Using_AwsAmplify/blob/main/lambda_function_final_with_db).4

**<mark>Note: In the Line number 14th, make sure to change the table name to your table name.</mark>**

# Step-8: Generate test traffic

Now we will generate a Test Event and will see if the output is getting stored in DB or not.

After test event trigger, move to DynamoDB page &gt; From left hand panel expand tables &gt; Explored Items and you will see our output. ☺️

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689221475854/7920a429-f065-43b0-ba3d-c5d2aa912dbe.png align="center")

We also need to put the **API entry point** to our *index.html* code.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689218430957/cf3070a6-314b-4983-b02a-5fefec64e918.png align="center")

As soon as you pushed the change, automatically it's getting deployed by AWS Amplify, which seems like a CD Pipeline with the webhook trigger.

It's truly a great feature I must say! Did you know that before? Let me know in the comment section.

🤩🤩🤩🤩 And finally, if you check your web app now, it's giving the result! ✅

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689220970411/6ab66c38-0c28-44df-86fa-bee6340c2736.png align="center")

If you made this till now, you are already an AWS Star ⭐✨. Treat yourself with something good today as you made it happen 🥰.

💖 Thanks for being with me till the end. I hope that I provided you with some useful knowledge. Don't forget to spread the blog to your friends and community. 💖

Feel free to ask any questions, I'm just a DM away.👍

### Follow *Sitabja Chatterjee* for more content! ✌️

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689221940025/0c0690a5-4387-4cb5-8c3e-6fd114cec6cf.gif align="center")