---
layout: post
title: "New ways to consume information"
date: 2015-10-21 08:10:37 -0400
comments: true
categories: 
---

After using puts to no end, I was curious to see what interesting (and practical) ways there are out there to output and consume information in Ruby. Inspired by a project idea from Avi, I looked into Twilio, a company that "allows software developers to programmatically make and receive phone calls and send and receive text messages using its web service APIs". (Wikipedia)

After signing up for an account and trial phone number on their website, it was easy to find documentation for their different APIs. I don't think they could have made the Ruby one any simpler:

![alt text](../images/102015/twilio.png)

I divided this into 2 methods and wrapped a class around it so that I could pass the message through.

![alt text](../images/102015/twilio-2.png)

I was kind of amazed to see it work right away. 

After sending a few texts, however, I noticed I had begun incurring a charge on my Twilio account for each one. 

![alt text](../images/102015/twilio3.png)

Paranoid that I was going to rack up a bill, forget about it, and end up with collections chasing after me for a few pennies, I reached out to Twilio support to figure out how I could pay the balance (there was no obvious way to do so on the website). While I was waiting for a response, I was pondering other possible delivery methods. What about email?

After some Googling, I found a quick and easy solution. Armed with a new Gmail account for testing, I took what I found and wrapped everything in a class with a send_mail method (this should probably be split up into more methods but I wanted to get it working):

![alt text](../images/102015/gmail.png)

Again, I was half surprised to see that it worked right away. Much to the dismay of several of our fellow students, I immediately began to spam some of them with email blasts containing various facts about sloths.

Shortly after implementing the mailer, Twilio's response came:

> Hello korey,
> 
> Thank you for reaching out! With a trial account we give you about roughly $30 of real credit to test with, but we do not expose balance in the UI until you upgrade.
> 
> Looks like you have about $28.00 left or so, until you would need to upgrade. We will notify you when your balance is getting low.
> 
> I hope that this information is helpful. Let me know if you have further questions
> 
> Regards,
> 
> Twilio Customer Support

So you don't need to worry about getting charged on a trial account until you hit about $30. 

Well, there you have it. Two cool ways to send information in Ruby. I recommend playing around with both of these, as they are both easy to setup and will quickly open up a lot of real-life applications to many of the things we have been learning. Have fun!