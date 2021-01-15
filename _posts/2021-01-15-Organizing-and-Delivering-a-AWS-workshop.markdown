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

