+++
date = "2015-12-27T14:33:21-08:00"
draft = false
title = "Polymer"
description = "My experience with Polymer"
tags        = [ "Development", "Polymer"]
topics      = [ "Development", "Polymer"]
+++

I heard about [Polymer] (https://www.polymer-project.org/1.0/) at a Google Meetup in Sacramento and immediately wanted to play with it. The ideas behind making such modular code were really amazing to see. With so much emphasis on using frameworks it was really refreshing to see something different. With Polymer you can plug it in to any existing frontend or build from scratch.

## Install

Installation of Polymer is pretty easy using [Bower](http://bower.io/). Package managers are really making installations a non-issue.

## Code

The Code for using Polymer is really easy to understand. Their example projects are very helpful with some good documentation. Where Polymer has some issues is they had a huge change in how Polymer was structured from 0.5 to 1.0, with this change there are still a ton of videos and links for 0.5 which makes finding answers a bit harder. Just keep an eye out for what version they are talking about and it should be fine.

## Deploy

Deploying was a bit more complicated for me. I was having some issues with the minimization of my JS. It turned out there was a bug in the version of Polymer that I was using. Once I figured that out deploy was easy, I set it up on my AWS server with no issues.
