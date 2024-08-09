---
template: SinglePost
title: Hello World
status: Published
date: 2019-07-21
featuredImage: https://ucarecdn.com/1e71932b-3bf9-45b0-8ec6-3667b20141a5/
excerpt: Welcome to the first post on my blog!
categories:
  - category: Personal
meta:
  description: Welcome to the first post on my blog! From here on, I'm going to
    share what I learned while doing my software projects and also post other
    stuffs that interest me.
---
Welcome to the first post on my blog! From here on, I'm going to share what I learned while doing my software projects and also post other stuffs that interest me. If you have interest on the topic that you are reading, be sure to check my other posts too. Enjoy reading!

![Thumbs Up GIF - MrRobot Yes ThumbsUp GIFs](https://media1.tenor.com/images/b7c6e2b66e9b08b7fbff24003a44529e/tenor.gif?itemid=12421377)

This is actually the second blog site that I made, the previous one was running [WordPress](https://wordpress.com/) CMS with [Apache](https://httpd.apache.org/) server on [AWS EC2](https://aws.amazon.com/ec2/) instance. I had to stop the instance because my free tier on AWS expired and I prefer not to stack up the bills with my other currently running instances, since I could use another free and fast hosting platform for my blog. Why not? 

On this Introductory post I'm going to talk about the reason why I changed my site framework entirely.

The blog that you are accessing right now is running on [Gatsby](https://www.gatsbyjs.com/), a fast React Framework that I connect to [Netlify](https://www.netlify.com/) CMS to ease up my writing and hosts it on their server. There are many of reasons on why I changed framework.

One of the reason is because of speed increase when loading my site, that you might have noticed, when you first open my site. This is because the whole site is a static webpage that uses a JavaScript library called [React](https://reactjs.org/) (developed by Facebook). React uses reusable components efficiently that's why I love it. Below is the screenshot of the result when scanning my website on [GTmetrix](https://gtmetrix.com/).

![GTmetrix result](https://ucarecdn.com/5c28e9a6-db47-4826-ad8b-e49907e289de/ "GTmetrix Result for my Website Speed")

The other reason is, since my website being hosted on Netlify, they have [CI/CD](https://en.wikipedia.org/wiki/CI/CD) feature included, which means every time I push any changes to my [GitHub](https://github.com/ilhamfadheel), it automatically pulls and deploys my site right there and then. And if I were to deploy a fail build, Netlify hosting would notice it and would not pull my fail build site and rather uses the last working deploy. I can't have an error build on my site ever! so I don't need to worry about screwing up my site. ain't that something?                       

 ![Wow Amazing GIF - Wow Amazing Great GIFs](https://media.tenor.com/images/12970068a5b7842a257b34088c5dcf36/tenor.gif)