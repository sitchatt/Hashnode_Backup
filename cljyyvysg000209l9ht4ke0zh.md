---
title: "AWS EventBridge with Shopify"
seoTitle: "Learn How to Integrate Shopify with AWS EventBridge"
seoDescription: "Learn how to integrate Shopify with AWS EventBridge for event-driven architecture. Follow this step-by-step guide by Sitabja Chatterjee and start triggering"
datePublished: Mon Jul 03 2023 00:04:23 GMT+0000 (Coordinated Universal Time)
cuid: cljyyvysg000209l9ht4ke0zh
slug: aws-eventbridge-with-shopify
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1688423695136/8f43430e-fff1-4086-8d92-a0ce4fc1e4ae.jpeg
tags: aws, aws-lambda, shopify, event-driven-architecture, aws-eventbridge

---

Hello Everyone,

Though, after a gap for educational and professional causes, again back with something very new, at least to most of you.

As you know, I love to explore new tools and technologies, exploring new AWS services and showcasing the use of those in the community is my all-time pleasure. 😊 So today, let's explore another great AWS services which might be **on-demand** in the near future.

It all started when I recently heard the term "**Event Driven Architecture**" in my current company project as it's new in the implementation phase, and I became curious and started learning about it.

Gradually I understood the basics of this architecture and how it helps in performance.

> *EDA encourages services and components to be loosely coupled. Events serve as the communication channel, enabling components to cooperate without being directly dependent on one another. Through this loose connection, components can develop independently, enhancing the system's agility, scalability, and ease of maintenance. As long as they comply with the event contract, changes to one component do not necessitate changes to the others.*

I'll try to add more points in my LinkedIn Post, here let's start with hands-on.😎

I've chosen **Amazon Eventbridge** for its various advantages over other cloud providers.

![](https://cdn-ssl-devio-img.classmethod.jp/wp-content/uploads/2020/01/amazon-eventbridge.png align="left")

> AWS Event Bridge Supports 3 types of event sources.

1. AWS inbuilt services
    
2. 3rd Party SaaS apps such as Shopify
    
3. Custom event
    

Here we gonna integrate Shopify, a popular e-commerce site, as input and we are going to trigger events.

Let's see what we can do.

## Step -1: **Integrate Shopify**

Search for **AWS Event Bridge** and click on the console. and from the left scroll bar, click on "Partner Event Sources".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688427333373/da47f1e3-44a1-4684-986f-31267e64495a.png align="center")

Then, search for Shopify and click on "**Set Up**"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688427458085/826538f0-8830-4ecf-8d1d-280a2847a1cd.png align="center")

Then, as per Step-1, save the account ID in a notepad, and as per Step-2, click on the Shopify Website Link.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688429112977/6bc7c7cd-5408-4b23-a8a9-eb180abf1b15.png align="center")

Register with your preferred method. I chose my email id. It's quite safe, so no need to worry.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688427858184/7ac00f85-c563-4c6c-b812-933c3d5e7b8d.png align="center")

Now click on, 'Create Shopify ID'

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688428099017/5dbe3e5e-516c-4dc6-9325-b976f914fe75.png align="center")

Now, click on "+ Create new partner account" and fill in all the details it will ask for. You can give any random input if you don't need it after this. I'm not posting each screenshot as it will make the blog unnecessarily long. For any issue, I'm just a LinkedIn DM away.

After this, it will look like below. Verify you are getting the same page.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688428410581/36c9c101-170e-4f39-ac30-69a39b35fc9b.png align="center")

## Step 2 : Create an App in Shopify

Click on Apps &gt; Create App

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688428613563/a9c12624-1658-4ba2-95cf-4d7345c6fefe.png align="center")

We are going to create the app **Manually** to test the event. Click on the option and give any name.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688428789012/bd4f62fe-4391-40a5-8ab3-6817dac1bb5f.png align="center")

Now, click on App Setup from the left bar and then go down the page and you will find the option "Amazon Event Bridge". Click on 'Create Source'.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688428948189/72b74653-7b9a-4b73-b8fe-2d93a9410125.png align="center")

Now, give the:

* Account Id you saved before in Notepad
    
* Region (I've chosen N. Virginia)
    
* Your desired name
    

Now if you come back to the AWS console and check the partner event sources, you will see newly create source is added.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688429401018/c521617e-f947-4c02-9fcd-8ab0f9a8e77a.png align="center")

Now, don't take the stress of its pending state, click on it, go inside, and then click on "Associate with Event Bus".

> The Event Bus in AWS EventBridge is a central messaging system that facilitates event-driven architectures and integration workflows by allowing communication and coordination of events between various services and applications within the AWS ecosystem.

When you click on "Associate", AWS will create a New Event Bus for you.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688429700286/ec9bde9f-bfcc-437d-825f-fa310cf19a62.png align="center")

You can go to "Event Buses" and check your Event Bus.

Now, Source is set, and Event Bus is set. What's Next?

> Think of it as a situation in NH. We left our home which is our source and we boarded a bus. Now, we need to know, where to land. In between there will be a toll plaza who having some rules and regulations to check and after checking only we can move forward to our target destination.

In the same way, we need to set up the Target now and also rules to pass to redirect events to different targets or ignore events as convenient.

## Step - 3: Creating Rules for Our Events

To Set up a rule, Click on Rules from the left bar, choose the correct event bus, and click on Create rule.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688430410916/32b4fe26-d36a-4d36-a0f8-39d6b72d74ec.png align="center")

Give Rule name, Choose Bus again, and click on next.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688430509962/2eb2b98a-9e13-48c5-866d-2936c086027b.png align="center")

Now, click on next and it's time to set the rule and the payload we are expecting. Click on the options shown in the screenshot. Then go to the [Github folder](https://github.com/sitchatt/AWS_Event-Bridge/blob/main/README.md) , move utmost down, and copy-paste the Shopify pattern and payload.

For payload remove unnecessary commas, you may get in line no 19. JSON format should show as Valid.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688432055388/02f1e046-2af0-4c17-8f81-5b0ed19839a6.png align="center")

You can click on the "test pattern" option (just above next) and if it's green, Click on "Next" and it's time to choose the target.

### Create a Lambda Function:

we will be using a lambda function as our target. So create a default lambda function.

After creating just come down and add the below line in the code and deploy.

```json
console.log('event:', event)
```

This line logs the value of the `event` parameter to the console before executing the rest of the code.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688432778289/02b7dd1e-bd40-440d-bec7-4cb44e12e458.png align="center")

Functionally, both code snippets perform the same task of returning a response with a status code of 200 and a JSON body of "Hello from Lambda!". The presence of the console.log statement can be used for debugging or logging purposes during development.

Now fill in the details as shown in the screenshot &gt; Next &gt; Next &gt; Create Rule.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688433001556/6389817f-03c0-46f9-b926-19e2d8ef55bc.png align="center")

Now finally 🤩 the whole integration is done. Sit Back, Have some water, and let's now test our project 💖.

> Move to Shopify, create a product and it should trigger the event. On the first go, you will not find the option to add product. You have to create a store first. I'm leaving it to you guys to explore 😶

Once done, you will see a new cloud log group is generated and the log showing there.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689118110486/19bc1dc5-ed89-4838-9d24-64009452a61e.png align="center")

Hurraaayyyy 🤩🤩🤩🤩🤩

Thanks for being with me till the end. I hope that provided you with some useful knowledge. Don't forget to spread the knowledge to your friends and community.

Feel free to ask any more questions or for help if you need it.👍

### Follow *Sitabja Chatterjee* for more content! ✌️

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689119224741/871c8974-3839-40f0-b156-8c3ff9674b1c.gif align="center")