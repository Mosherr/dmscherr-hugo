+++
date = "2018-12-02T16:12:21-08:00"
draft = false
title = "QuoteBot"
description = "QuoteBot"
tags        = [ "Development", "Go", "Mongo", "Heroku"]
topics      = [ "Development", "Go"]
+++

## My Goals:
Learn GO <br>
Spend no money <br>
Build a Quotebot for Slack <br>
Make it easy to use <br>
Make sure it is expandable <br>
Open Source it <br>


## Getting Started:
I needed a project to work on in order to teach myself how to code in GO. At my company we started using GO on modular pieces that tie into our main code base. My colleague at work was spearheading that project and I wanted to be involved, but requirements and timing made it hard to do. I figured if I wanted to learn I needed to find my own project. Conveniently, a group of friends that had been using IRC for chatting recently moved over to slack. One of the things that slack was missing that they wanted was a QuoteBot, a plugin that allows saving and recalling of silly things said in the chat room. I decided this was the perfect chance for me to learn GO, as well as some other technologies along the way.

## The Tech:
I decided I would code the project in GO using a MongoDB to store all of the quotes then host it on Google App Engine. I found a simple slack bot example that served static quotes; this was a great starting point for me. I was able to get that bot up and running with no problems. It took a little planning to figure out how I wanted this QuoteBot to work, such as what commands did what and how I would handle validation.

## My breakdown of this project:
Create a slack bot that allows serving of static quotes <br>
Add database support <br>
Include metadata on quotes (quoted user, user who added the quote, date added) <br>
Make it so the quote returned is random <br>
Allow a user to be specified and only return quotes by them <br>
Allow adding quotes <br>
Optimize code <br>
Release <br>
Gather feedback <br>
Optimize use <br>
Import old quotes 


## Implementation:

I started by adding a get command that would return a random quote from a static array. I found a really good sample slack bot written in GO for app engine. I was able to get this app up and running locally pretty easily. This code only allowed serving a random static quote from an array. The first thing I changed was to add a more advanced request handler that would parse the slack slash command for command tokens. The first token was -g which would get a random quote. <br>
The next step was setting up a database so the content could be dynamic. I decided on [Mlabs] (https://mlab.com/) based on a recommendation from an [App Engine tutorial] (https://cloud.google.com/appengine/docs/standard/go/building-app/storing-data).  The setup was easy and I got half a GB of storage for free. I was able to manually insert a quote and get it by calling my App Engine endpoint. <br>
The next problem was that the quote returned was just the first in the Db, so I had to figure out how to get a random quote. I was able to make it work by making a call to get the total count of documents matching the filters on my query. I would then generate a random number from 1-n where n is the number of quotes that match the filter. I took that number and added a slice to my mongo query to get a random quote. <br>
The next step was to allow getting a quote from a specific user. I decided to use the slack autocomplete user tokens. I made it so -g @user would now return quotes from a specific user. This was a fairly easy addition for my mongo query. I had to make sure I updated my count so I would get the correct number of documents for just the user in question. <br>
I needed to figure out how I wanted to handle adding quotes. With the Slack slash commands I was a little limited in my implementation of this and the best I could come up with was to add a command -a @user “quote text”. This ended up working well and I added some minimal validation that requires 3 arguments for it to work. The quote itself needed to be wrapped in quotes and I was not validating that the 3 arguments were actually valid, just the first one was -a which means add quote. <br>
I now had a working quotebot that locally did all of the basic operations needed. Now I needed to figure out how to release it on App Engine and tie it to our slack group. This is where I had the most trouble on this project. I was able to deploy the project successfully, but when I tried to use the slash command I would always see a 500 timeout error. I tried calling the API directly from a REST client but got the same result. I tried debugging this issue for a few days. I checked credentials, added debuggers, googled all the errors, tweaked firewall rules, contacted customer support, accidentally committed my credentials to github, created new credentials, tried App Engines Mongo service. I could not for the life of me figure out the issue. <br>
I became pretty frustrated and ended up talking with a colleague who recently earned his CS degree. He told me that all the cool kids were deploying applications to [Heroku] (https://www.heroku.com/) and I should check that out. Initially I was hesitant because I really wanted to solve the problem myself, but after several more failed attempts and staring blankly at the screen for awhile, I looked into Heroku. Heroku was really impressive, I found some examples and tutorials and was able to get the app deployed and running in a couple of hours. As a perk I learned a little about [Docker] (https://www.docker.com/) in the process. <br>
The app was now deployed, tied to our slack group and working. I told a few people about it and showed some examples. Initial response was slow but I received good user feedback. I updated the insert logic to prevent saving duplicates. I added a longer timeout since the free tier of Heroku will sleep servers if they are not in use so it takes a little on the first request for it to wake up. I also removed the need to wrap the quote text in quotes. <br>
The last part of this project is to import all of the old quotes from IRC into the new database. This would take a little work to parse and map them to the current users in Slack, but thankfully I decided to give this part of the project to my friend who recommended Heroku since he wanted to help. <br>
Although the deployment phase of this project was frustrating, I had fun working on it and learned a lot. I was able to take the knowledge I gained working on this project and apply it to my job. I was able to work on a few more complicated issues in GO with much more confidence than I had before. Overall, I really like GO as a programming language and in the future if I work on any new projects I will write them in GO.

## Why GO?
I Chose go because it is a great up and coming programming language that has a lot of potential. I wanted to make sure I understood how it work and could comfortable write code using it. My company also has some micro services using GO that needed maintenance and this project game me the knowledge to work on those services.

## Why Mongo?
Mongo seemed like a natural choice for a quotebot since there was no need for a relational database. Mongo could easily and quickly serve quotes. I also wanted to get more experience with NoSQL databases.

## Why App Engine/Heroku?
I originally picked App Engine because I was looking for something free that I could deploy to, if the project went well I would get a paid server. App Engine gave me so many headaches I decided to use Heroku instead and was very happy with the results. 
