---
layout: post
title: "Thank you, swipe again"
date: 2013-07-23 17:25
comments: true
categories: 
---
So I'm writing this because the media seems to be making a huge deal out of Tinder's privacy issues. (read [this](http://qz.com/106731/tinder-exposed-users-locations/) and [this](http://valleywag.gawker.com/your-tinder-account-was-vulnerable-and-they-never-told-885675272?rev=1374611580&utm_campaign=socialflow_gawker_twitter&utm_source=gawker_twitter&utm_medium=socialflow)).

I discovered the issues at the Branch hackathon last weekend (props to [@hursh](http://twitter.com/hursh) and the rest of the kickass team at [@branch](http://twitter.com/branch) for throwing an amazing hackathon).

Here are the facts:

* Yes, Tinder was releasing geolocation and Facebook data through their private API
* Yes, it let you do some remarkably creepy things (like [this](https://www.dropbox.com/s/1seoi7i2g9mj8qg/Tinder%20-%20Broadband.m4v))

However, unless you know how to set up a [mitm](http://en.wikipedia.org/wiki/Man-in-the-middle_attack) proxy, it's simply not possible to grab that data. I'm going to assume that doesn't qualify as a "simple hack" as the majority of the media put it.

There's a little in Sean Rad's response that I don't agree with. However, his reasoning for not bringing it to the user's attention is valid - “It was a minor flaw that didn’t impact any of our users, so we decided it wasn’t worth bringing to their attention.” 

Not only was the API private, but I've never seen a company fix an issue that fast. I think I emailed them at 4am. When I woke up, it was fixed, and for that, they seriously deserve to be commended. They say they take their users' privacy seriously, and it looks like they mean it.

As to why that data was in the response in the first place, I'm hesitant to believe that it happened during the Android rollout. I'd say it's more likely that they calculated shared friends, likes, and distance client side instead of server side for the early versions of the app. When they switched to server side, they never removed the raw data.

**Updated:** They called me last night to say thank you. They wanted me to speak with the CTO, but he was busy working all night to look for and fix any further privacy issues. Yes, Tinder messed up, but their response has been phenomenal and I'm thoroughly impressed.

Comment on HN [here](https://news.ycombinator.com/item?id=6102624)
