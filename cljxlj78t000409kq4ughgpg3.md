---
title: "A Guide to Amazon Lex and AWS Lambda Integration for Seamless Conversations"
seoTitle: "Efficient Chatbot Integration: AWS Lex, Lambda, CloudWatch"
seoDescription: "Streamline chatbot integration with efficient AWS Lex, Lambda and CloudWatch. Optimize performance, monitoring, and scalability for seamless user experience"
datePublished: Mon Jun 19 2023 01:10:09 GMT+0000 (Coordinated Universal Time)
cuid: cljxlj78t000409kq4ughgpg3
slug: a-guide-to-amazon-lex-and-aws-lambda-integration-for-seamless-conversations
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1689035788898/cd84f7d8-7012-4348-bf8b-6cd211966e12.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1689037266400/28a76e53-d791-486f-bae3-7286aa11f0c8.png
tags: aws, amazon-web-services, aws-lambda, aws-cloudwatch, aws-lex

---

Hello Learners, Hope you all have successfully built a chatbot using Amazon Lex.

If you haven't, go through Part 1, and click [HERE](https://sitchatt.hashnode.dev/create-chatbot-in-5-minutes-with-amazon-lex) .

In this blog, we will show, how to actually run the bot in a serverless approach. Also, we will use **AWS Cloudwatch** Service, to view our logs.

## 🎯AWS Services used:-

> 1. Amazon Lex
>     
>     ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689035829886/529151a4-a27f-4d71-9d65-3bf2df60d037.png align="center")
>     
> 2. Aws Lambda
>     
>     ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689035847502/5582cebd-94c0-4270-ad6f-02608e0cbbb7.png align="center")
>     
> 3. Amazon Cloudwatch
>     
>     ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689035894144/bdaf5f0d-f84a-4af3-8c0e-ced17ea43ff0.png align="center")
>     

  

So let's get started.

# Step - 1: Create a Python Lambda function.

Create a lambda function for our bot. I've chosen Python 3.8 version here.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689004195479/f75a6edf-2c13-4fd7-b61c-35557b3545f5.png align="center")

Now we need to add our Python function here. As we only created order intent, I'll add only the order function here. If you have created an intent for order and cancel both, you can check the whole code [here](https://github.com/sitchatt/Chatbot-Lambda/blob/main/lambda_function).

The code is having discounts and other stuff.

> ©️ Code credit goes to - Architecture Bytes

Now Just update your code as shown below. And "**Deploy**"

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689006469942/6c8ded40-062c-44a0-bfd2-c7afc72a3a1b.png align="center")

# Step-2: Configure Lambda on Intent

Go to the intent, for me it is "**CreateOrderIntent**".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689031221307/7847bf8b-2324-4c65-a0c9-9efd6a6939cd.png align="center")

Expand the fulfillment &gt; Click on Advanced Options &gt; chek the box "Use a Lambda function for fulfillment" as shown above.

Then update the intent.

# Step-3 : Create a bot version with alias (Not Mandotary)

Till now we were using the demo version, it's time to create our own version.

Move to "bot versions" and "Create version". Note, it's not a mandatory step, I added it to let you all know about it as it will help in reducing the downtime in scenarios where modification and re-deployment are required.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689031655291/c733a94c-b53b-45c5-973a-f5b0a327c03b.png align="center")

Then simply go down and click on "Create".

You can see, now we have our own **Version 1**.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689031800295/68846f50-e1e8-467f-abef-32cb5fafc3cc.png align="center")

Now, we will create **Alias**.

> In Amazon Lex, an alias is a label or reference to a specific version or snapshot of a chatbot. It helps manage multiple versions of the chatbot and allows you to control which version is active or live at any given time. Aliases are useful for A/B testing, gradual updates, or maintaining different versions for different environments. By assigning an alias to a version, you can update the chatbot by publishing a new version and redirect the alias to it, without modifying integrations or endpoints.

To create an alias, follow the below steps.

> Move to Alias Section &gt; Create Alias &gt; Give a name &gt; Choose the version (For us it's Version 1) &gt; Create

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689032083205/ad1a8e4d-5413-4c36-b0eb-c7bf58aa3a7e.png align="center")

Now , go to our newly created alias and click on the language **"English US"**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689032240565/083d5218-6b8f-4eb6-abf6-90b32d01efd5.png align="center")

Now, in the source, give our function name and the version will be selected automatically as $Latest which is like a variable that will take the latest version always.

Click on **Save**.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689032329059/88d8dc13-345e-445d-9625-e8f6ba747095.png align="center")

A Snapshot of your work is saved with the lambda function active. You can use that while testing the draft version.

Now, You guys may face an issue 😶that I faced! Let's learn how to troubleshoot that also.

# Troubleshoot Error :

> As we all know, my purpose here extends beyond showcasing finished work. It is my genuine commitment to care for my fellow learners and our community. I encountered an error that led me to reflect on its nature and explore potential solutions.
> 
> Driven by my desire to help, I diligently troubleshooted the issue. Now, I feel compelled to share this information with all of you, ensuring that everyone is aware and equipped with the knowledge to tackle similar challenges.

So now, as already you have built the draft version, it has the lambda function integrated it may seem.

So, now if you just simply try to test, it will throw you an error like this ;

`Cannot call FulfillmentCodeHook for Intent CreateOrderIntent. BotAlias/LocaleId TestBotAlias/en_US doesn't have an associated Lambda Function.`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689033206802/1c6a1db0-cf9c-41bc-a7ae-cd80f6ea1e11.png align="center")

If you read the error message, it shows that our test alias still hasn't been associated with a Lambda function. Remember It's about the Test draft Alias. For version 1, we have added the source already.

To resolve the issue, we will simply associate our lambda function with this alias too, simple :).

To do this, click on the gear icon at the top right corner of the chat box.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689033383594/166e7d02-eff1-4ac5-8bd2-cb35f1a06aa2.png align="center")

Add the source here and "**Save**".

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689033475195/900744b7-97dd-470a-9394-d519c5a35810.png align="center")

### And Boooom! 🎉You can now see the output is coming as per the lambda function! 🤩😍

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689036742807/d97d77a1-7de4-4378-b0ce-cacd861c05c6.png align="center")

If we want to confirm, whether the lambda function is working or not, simply go to **AWS Cloud Watch** and you will see a new log group is automatically created. ✌️✌️

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689034484269/a55909f3-48a9-43ba-bb29-1e606138d23f.png align="center")

These are the logs generated for this function.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689035196393/59db1970-72c8-4637-9fef-67eac9c8f86e.png align="center")

💡Any modification or contribution to this is highly appreciated.

💖 Thanks for being with me till the end. I hope that I provided you with some useful knowledge. Don't forget to spread the blog to your friends and community. 💖

Feel free to ask any more questions or for help if you need it.👍

### Follow *Sitabja Chatterjee* for more content! ✌️

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689036979632/e8a083c1-3aa9-4cd9-a568-a24b03a10fbc.gif align="center")