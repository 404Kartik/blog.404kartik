---
layout: post
title:  "Hosting a custom Sub-Domain with GitHub"
description: Hosting your sub-domain while retaining your brand
date:   2020-08-23 21:03:36 +0530
categories: Jekyll Github DNS
---
If you’re anything like me then you probably have one big Maximum Linux Hosting account with 100+ subdomains running all kinds of different websites.
I love using GitHub Pages for static sites in particular because all it takes to get your site live and make updates is a quick ``git push`` command. In fact, I just uploaded my personal portfolio site to GitHub Pages last night and it took less than 5 minutes.

You have a domain hosted on Namecheap, and you want to point its DNS to your website hosted on GitHub.


1. Let's start with the website you want to bring online. Select your desired code repository, then go the **Settings **tab.

2\. Scroll down to the **GitHub Pages **section.

3\. Under **Custom domain**, add your domain.
![A test image](/assets/gh.png)

4\. Login to your Namecheap account. Navigate to **Manage Domains**.

5\. Scroll down to your desired domain, click through to the next page, then scroll down and select **Manage DNS**.

6\. Once you're in, you will want to add a CNAME Record with the following values (where **Points to** is [YOUR USERNAME].github.io):
![A test image](/assets/name.jpg)

**WARNING:** If you already have a CNAME Record with **Host **set to **www **it won't let you create a new one. So either delete or modify the old one with the information above. You only want one at the end of the day.

It should look like the following when you click Save (with your username, of course).

GitHub Pages should automatically create a matching CNAME file in the root of your repository that points to your desired domain. If not, create one.

If you can't figure it out. Don't worry. It's not hard. Create a file in GitHub called CNAME and on the first line type in your desired custom domain. But you probably won't have to do this.
Make sure that your CNAME file is exactly like this
![image](/assets/CNAME.jpg)

Your site should now be live, hosted entirely on [GitHub Pages][3]!

##Now you would like to deploy your website to the s3 bucket
You need one of your s3 buckets configured for static web hosting for this deployment. Read my story on s3 static website deployment and configure one if you don’t have.

Automatically deploy changes made to the GitHub repository of the static website to AWS S3. The change you make will be instantly available on live website yourdomain.com.

You don't need to clone the git repository to make changes. You can do it from the github.com website itself. After configuring the pipeline, you don't need to login to AWS. Everything happens automatically under the hood. Aint it cool?

You need one of your s3 buckets configured for static web hosting for this deployment. Read my story on [s3 static website deployment][2] and configure one if you don't have.

Login to [AWS console][3] and go to [CodePipeline][4].

**Important**! Switch to the correct AWS region where your S3 website is created before creating the pipeline.

Click the **Create pipeline **button.

Give the **pipeline **a meaningful name: _web-s3-deploy_  
Select **New service role**. Give it a meaningful name: _web-s3-pipeline-role  
_Artifact store: Choose the **Default location** option  
Bucket: select the s3 bucket which the **static website** is hosted.   
Hit the **Next **button.

Select the Source provider: **Github**.   
Click the **Connect to Github **button. Authenticate Authorize AWS CodePipeline to access your Github Repos.

After authentication, select the Repository with your static website files. Select the branch of the repository. _I'm using a static website noobcod.com for this tutorial._

Select the **Github webhooks (Recommended)** option. **Important!** You need to be the **owner **or an **admin **of the repository to create webhooks.

Hit the **Next** button.

Hit **Skip Build Stage **button. _You can use AWS Codebuild to compile typescript or any project that need to build before deploy. We skip this because the repo contains static website contents._

Hit the **Skip **button on the prompt.

Deploy provider: Select **Amazon S3**  
Bucket: Select the bucket which configured for the **static website**.   
Extract file before deploy: You **must check **this because code pipeline compresses the artifact.

No additional configurations needed. Hit the **Next **button.

You can go back and change configuration if you made any mistake at the Review step. Hit the **Create Pipeline** button.

Go to your domain from the web browser. It's now deployed.








