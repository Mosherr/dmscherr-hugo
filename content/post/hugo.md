+++
date = "2015-12-27T14:33:21-08:00"
draft = false
title = "Hugo"
description = "My experience with Hugo"
tags        = [ "Development", "Go", "Hugo", "Blog"]
topics      = [ "Development", "Go"]
+++

After a recommendation from a friend I decided to take a look into [Hugo](https://gohugo.io/). Hugo is a blog framework built on Go. I have been trying to find projects in Go so I can learn more about it so this seemed like a good start. I decided to take down my old site which was just a resume and profile for a blog. I've had prior experience with Drupal and Wordpress - they are great platforms, but I wanted something with less bloat so I decided to go with Hugo.

## Install

Installing Hugo was very straight forward. [Brew](http://brew.sh/) makes life much easier.

## Code

Coding took a little while to figure out but the documentation is pretty good and once you get started things are fairly simple. Unless you really need or want to, Hugo abstracts a lot of the code, almost all of it, from creating and managing a blog. It is a little more developer focused then Drupal or Wordpress but it is still very easy to use.

## Deploy

Deploying was probably the hardest part of Hugo for me, not because the process itself is hard but finding the information was not as straight forward as I would like. I have noticed that with a lot of [Getting Started](https://gohugo.io/overview/quickstart/) documentation it walks you though development and setting up simple application to run locally but then no info on actual deployment. Eventually I found how to build my Hugo project for release which was pretty neat. All of the static HTML generated and ready for deployment. I ended up setting up an [Amazon S3](http://docs.aws.amazon.com/AmazonS3/latest/dev/WebsiteHosting.html) bucket for hosting my static site which is cheap, easy, and amazing. I was able to follow the steps to set up the S3 bucket and point my DNS from [Hover](https://www.hover.com) to it with no problem. After I did the first deployment manually I set up [Werker](https://app.wercker.com/) (which I always see as Wreker) to handle automated deployments. I will write separate posts for Werker and my experience with S3 Static Web Hosting in later posts but I am pretty impressed.
