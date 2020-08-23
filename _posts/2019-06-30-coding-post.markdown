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
![A test image](gh.png)

4\. Login to your GoDaddy account. Navigate to **Manage Domains**.

5\. Scroll down to your desired domain, click through to the next page, then scroll down and select **Manage DNS**.

6\. Once you're in, you will want to add a CNAME Record with the following values (where **Points to** is [YOUR USERNAME].github.io):

**WARNING:** If you already have a CNAME Record with **Host **set to **www **it won't let you create a new one. So either delete or modify the old one with the information above. You only want one at the end of the day.

It should look like the following when you click Save (with your username, of course).

GitHub Pages should automatically create a matching CNAME file in the root of your repository that points to your desired domain. If not, create one.

If you can't figure it out. Don't worry. It's not hard. Create a file in GitHub called CNAME and on the first line type in your desired custom domain. But you probably won't have to do this.

Your site should now be live, hosted entirely on [GitHub Pages][3]!


```javascript
const express = require('express')
const app = express()
 
app.get('/', function (req, res) {
  res.send('Hello World')
})
 
app.listen(3000)
```

Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aliquam qui voluptatem excepturi nemo similique atque sapiente aperiam, dolorum deleniti! Esse quam perferendis temporibus nemo at molestias necessitatibus tenetur cupiditate sapiente. Lorem ipsum dolor sit amet, consectetur adipisicing elit. Nihil et voluptatibus non labore officiis assumenda, distinctio perspiciatis blanditiis nesciunt rerum molestias impedit fugiat nulla qui libero minima quasi! Libero, iure.

```scss
body {
	font-family: 'Nunito Sans', sans-serif;
	line-height: 1.5em;
	margin: 0;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
}
```
Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aliquam rerum, ratione impedit necessitatibus facere soluta odio repellat asperiores neque! Sunt iusto quia suscipit amet inventore eum, vel molestiae reiciendis alias.
