---
layout: post
title:  "Organizing, Developing and Delivering an AWS workshop"
description: This blog talks about how I delivered 
date:   2021-01-15 21:03:36 +0530
categories: AWS Workshop Developer Cloud
---
#### We all know how important the cloud is in this era of tech, educating students and my mates about this power is something which I really enjoy. Which led me to team up with some of the great mind at AWS itself to deliver a workshop

### How it all started?
In September I helped my peers organize a workshop in Monash University and Univeristy of Melbourne, which led me to take an initiative at my University ( RMIT University ). My mentor ( Paul ) set a challenge for me to develop my own web-application, document it, make slides and deliver it in 8 weeks. I was super pumped by the challenge. This was a really great challenge for my personal growth and giving to the community as well.

### What I developed?
I began brainstorming ideas, I knew that I always wanted to build something which involves AI and Machine Learning to make it really interesting. 
One of the challenges while building this thing were that not only it has to work properly and be good, it also has to be something appealing to someone new to it. Even a Finance major should be able to find it fascinating.
![A test image](/assets/architecture.png)
###
So I began work, 
I used AWS Cognito, Elasticsearch, Appsync, Graphql, S3, Amplify and Rekognition to develop a full stack AI powered web-application which uses : 
* AWS Cognito - For authentication and User pools
* Elasticsearch - For searching through labels of photos
* Appsync - Fetching names of the albums
* Graphql - Storing names of the albums and S3bucket locations
* S3 - Storing images
* Amplify - Bringing everything in this architecture together
* Rekognition - Generate labels using pictures ( lambda function )

### Documenting 
As developers we are doers and most developer I know hate documenting, but sooner or later I see everyone realizes that as much as it is important to write clean code it is to know how you wrote it.
Documenting this workshop was a challenge in itself as not only this was to be documenting the code, it was documenting the whole process of this architecture. Which sounds simple but showing someone the diagram of an architecture is way different to actually sit down and write how to provision it.
So I used Hugo ( a static website generator ) to document the process and had to do my own workshop atleast 30 times before I had it fully documented.
#### Link to documentation : tinyurl.com/awsxrmitlab

### Organizing
Now that everything on my part was ready, it was time to bring people together and decide upon a date to deliver this venture.
Bringing everyone together is probably on of the hardest things as everyone has their schedule and everyone works full-time. So getting everyone on-board was a challenge in itself.
For this I had to create slides and documents which made everyone understand the process in an easy way.

### Marketting
People attending your event makes your event what it is, in my expirience I spent more time marketting this event than any other thing. I won't say it is the hardest part of organizing but it is definetly the most time consuming part of it.
I contacted my university clubs to send out emails about the event and suddenly we had lots of students registering. But even after having 100 registerations because the golden rule of event turn ups is that only 40% of the people of who register show up to a free event. This applied here as well. My aim was to get 150 students attending the workshop. Which was not impossible but was a challenge for sure.
## 
I did have a back up plan for this, one of my university professor ( prof. Fabio ) has always been really helpful to me. I contacted him for help explaining what the event was about and what we as a team plan to get out of it. One of the things that he appreciated was the we had a clear agenda, of what we want to do. This was not a marketting campaign for AWS. This was a workshop presented by a university student himself.
He escalated my request to the Associate Dean of the school of Computer Science and IT and they agreed to send out emails to every single student in the faculty who is studying anything remotely to IT.
##  
This incident gave the registerations a real boost. It was just a matter of days we had 320 registerations, which implied almost a 150 student turn up. ( Fun fact : 160 students turned up )

#### My general take
I will go into details on all these topics, just wanted to put my general thoughts into words about all these aspects about the event I organized. In the next few blogs I aim to put light on some of these topics individually.
My take about this event was that if you are ready to take initiative then things come together automatically for you. You just have to start the engine, put your thoughts into Driving gear fueled by your actions and you get a smooth drive all along.
####
Don't hesitate to reach out to me
Have a nice weekend!

