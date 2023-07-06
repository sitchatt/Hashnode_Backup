---
title: "Create ChatBot in 5 minutes with Amazon Lex"
seoTitle: "Effortless Chatbot Mastery: Harnessing Amazon Lex's Simplicity"
seoDescription: "Discover the simplicity of creating powerful chatbots with Amazon Lex. Elevate user interactions and maximize efficiency with effortless development."
datePublished: Mon Jun 12 2023 01:37:48 GMT+0000 (Coordinated Universal Time)
cuid: cljqhcr1200000al1hchy68iz
slug: create-chatbot-in-5-minutes-with-amazon-lex
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1688606058022/84e9bd9f-1a68-44cf-b23f-a45fabd7df73.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1688607198941/c973d16a-c3dd-42fe-8e1e-1389d203e839.jpeg
tags: aws, aws-lambda, amazon-lex, 5-minute, create-chatbot

---

Hey learners,

This week, I'm back with another helpful AWS service called Amazon Lex, which enables businesses to design chatbots that can also be voice-controlled and are extremely versatile in their development.

# Introduction:

![](https://tse1.mm.bing.net/th?id=OIP.EVp-OZPmyi01mYDJbEhzfgHaEK&pid=Api&P=0&h=180 align="left")

Conversational interfaces have become increasingly popular as a way to interact with consumers and deliver seamless experiences in the modern digital era. Amazon Lex, a powerful service by Amazon Web Services (AWS), has emerged as a game-changer in the realm of conversational interfaces. The creation of chatbots and voice-based applications is made easier with Amazon Lex's superior natural language understanding (NLU) features and seamless platform connectivity.

Now, let's talk about the components we need to set up while building a chatbot in Amazon Lex.

# Components:

1. **Intent:** An intent is a particular task or action that a user wants to carry out as a result of their communication with the chatbot. It symbolizes the underlying intent or significance of the user's input.
    
    In simple terms, an "Intent" is a 'goal that the user wants to achieve'.
    
    e.g. - Order a Pizza, Book a hotel, etc.
    
2. **Utterance:** An utterance in Amazon Lex is a particular word or input that a user gives to communicate with a conversational bot. It simulates the vocabulary and idioms that users might employ when interacting with the bot.
    
    In simple terms, an "utterance" is 'Anything a user says".
    
    e.g. - I want to book a flight from New York to London, etc.
    

![](https://image.slidesharecdn.com/4-170605230046/95/exploring-the-business-use-cases-for-amazon-lex-june-2017-aws-online-tech-talks-5-638.jpg?cb=1496706673 align="left")

1. **Slots**: Slots are used to capture particular data from users during a discussion, including names, dates, or numbers. They specify the data's structure and give the bot the tools it needs to accurately interpret and respond to user requests.
    
    In Simple terms, Slots are "Values provided by users, to fulfill an intent".
    
    e.g. - Chocolate(flavour), India (county), 5 (number).
    
2. **Fulfillment**: Fulfilment is the process of acting or responding to the user's purpose and the gathered slot values. It entails carrying out the required logic to satisfy the user's request.
    
    In simple terms, it kind of response to user input.
    
    e.g - Suppose one user says cancel the order, the chatbot will respond with, suppose, "**cancelling an order**". That's a fulfillment of the intent.
    

Also, there is a term associated with fulfillment, which is ***Confirmation.***

Before proceeding with fulfillment, confirming a user about the current status is called "**Confirmation**".

e.g. - "We are now ready to place an order"

> Mostly Chatbot runs through the **Lambda** function.

![Image taken from internet and used for educational purpose.](https://cdn.hashnode.com/res/hashnode/image/upload/v1688590118731/3f39505e-b6ab-4b64-996b-816a226e5805.png align="center")

In this blog, we are going to create a Chatbot first and then will test it.

# Step 1:

Let's now move to the Amazon Lex console.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688596675896/499d7c46-73e9-4bad-9360-830a725d3953.png align="center")

Now, let's make our Pizza bot 🥳. Click on **Create bot**.

* Name the bot as your wish
    
* Choose **Create a Role** option, which will create a new IAM role with the required permissions. You no need to worry.
    
* Choose **NO** for COPPA as we are doing it for demo purposes.
    
* Session timeout section we are keeping by default. You can change as per your convenience.
    
* Click on Next.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688597253858/71a4309d-711b-4fd6-892a-771db7080977.png align="center")
    
* If you want to change something such as language or Text-to-Speech voices, you can do and click on **Create**.
    

# Step 2 :

Now our main work is starting. Be creative as much as you want here 😁.

We will create our intent first.

I'll share the screenshot for the first intent with the logic behind it. For others, I'll discuss the logic only, so the blog will not be flooded with screenshots. For any help, I'm always just a DM away 😊.

## Welcome Intent:

This intent will serve as the welcome prompt, and it will be followed whenever a user writes for the first time. We now need to educate the bot based on our best guesses of the sentences that people might say. Users might, for instance, begin their message with "Hello" or just write, "Help me with a pizza." We must provide as much as we can.

* Give an intent name. For us it's ***WelcomeIntent***. Remember space is not allowed.
    

Now simply come down a bit and under **Sample utterances,** Add your sentences which will trigger the bot to respond.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688601032869/4023e915-07c8-4f40-8f01-21ccb61e4b49.png align="center")

* Now think as user interacted with the bot. Now bot needs to reply to user back right?
    
    Just below the utterance, there we can find **initial response** section, where we can set the bot response.
    
    You can create a simple response. Also, you can set something interesting 😎.
    
* Expand the ***Advanced Options &gt; Expand the "Response for acknowledging the user's request" &gt; More response options &gt; In the message group section, add a message &gt; From Top right side 'drop down' &gt; Choose card group &gt; Give the Title (****For us it's "*Hello, Welcome! What would you like to do?") **\&gt; Expand the "Buttons" &gt; Add buttons in key-value format &gt; Update response**
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688600040245/0311e5e3-943e-4f87-bad7-cbc5f2dc4652.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688599102371/7a7ccbca-e4f9-43ee-b613-a2eb877478f4.png align="center")
    
* Close the dialogue box and click on **Save intent**.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688599268268/49701576-17c6-423d-9bb8-3e33ed851bd5.png align="center")
    
    > **Note:** I'm only showing a way to make it. Explore and show the community your own creativity💖.
    
    Congratulation, 🎉🎉 our working chatbot is ready on a basic level and I can't wait to interact🤩 Let's see how it's working.
    
    # Step -3: Build and Test
    
    Simply click on build and then test to go for a demo.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688599671658/3cc2fb17-0138-4cae-8cf3-1b29dc397df2.png align="center")
    
    And here you go 😍. You can either type or use text-to-speech to speak and hear the responses.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688600128953/d8741ac7-0353-4bb2-b296-2836c00cb089.png align="center")
    

Now, I'll make add slots also to make it more interactive. To add slots, we need to create a new intent. Let's make it!

# Step 4 - Add Slots :

* Back the page and click on "Add Intent" &gt; Add Empty Intent
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688600673205/7e36c1c4-79db-4ad8-a77c-af8c5a7a2455.png align="center")
    
* Give a name and add.
    
* Provide Sentences, initial response and now come to slots.
    

**Logic**: Here we are creating an intent for taking orders. So sentences will be something as "Order a pizza" , etc. And Initial response we can say as "Sure!"

In Slots, Now we need to give some Slot types which will kind of work here as input variables.

Suppose, the slot type is **AMAZON. Date.** Anytime the user will provide a date as a response, this slot will take place there.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688601468430/aef72fbb-7073-405c-9613-53424ed508f7.png align="center")

This is our slot for Name. Like ways, you can create many slots. If any particular slot (such as flavour), is not available, particularly to Amazon, you can use **AMAZON.AlphaNumeric** which will take any random response.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688601910065/6d222e62-a455-41f0-8c08-62d7ec400f0c.png align="center")

You can also give them the choice to select, from **Advanced options.**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688602094026/52166bc2-2ba3-487f-a276-9b162f086fa0.png align="center")

# Step 5- Confirmation :

After all the slots added, we will go for ***Confirmation*** section. Toggle the bar and make it active.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688602842907/c2209732-361f-4204-b89d-6212b2403442.png align="center")

Now, we know what to say when the user will respond with "NO". But if the user says "YES" to the order, then?

Yes, you guessed it correctly! It will then move to the "***fulfillment"*** section.

# Step 6 - Fulfillment :

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688602988697/d288cc86-073f-428e-99de-8424017fd3a5.png align="center")

Now, give a closing statement also for a good closure. and **Save Intent!**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688603146883/63489001-61a6-4ceb-afe1-f6fb08849d17.png align="center")

You can create a new intent for "Cancel Order" also. I'm not showing that here as the process is exact same and moreover I'm very excited to see you guys in a LinkedIn post with an updated chatbot!

# Final Test :

> ### Let's Build and Test our Final Product! 😎❤️🔥

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688604782824/8c98debb-deb6-4414-9d71-721a410b52e5.png align="center")

It's Just perfectly working, even with voice notes. 🔥🎉.

# Conclusion:

There are many advantages to using Amazon Lex for creating conversational bots and NLU capabilities. With its built-in language processing, intent recognition, and slot-filling features, developers can easily build chatbots that comprehend and effectively handle user input. It also has a seamless connection with other AWS services like Lambda and S3.

Additionally, Amazon Lex simplifies the development process, reducing the time and effort required to build conversational interfaces while providing advanced features like context management and session handling. Overall, leveraging Amazon Lex empowers developers to create powerful and intelligent conversational experiences with ease.

Thanks for being with me till the end. I hope that provided you with some useful knowledge. Don't forget to spread the word to your friends and community. Part -2 is coming very soon!

Feel free to ask any more questions or for help if you need it.👍

### Follow *Sitabja Chatterjee* for more content! ✌️

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1688605113698/bc6391a3-e00d-4b8f-8cc2-25b6a336ceba.gif align="center")