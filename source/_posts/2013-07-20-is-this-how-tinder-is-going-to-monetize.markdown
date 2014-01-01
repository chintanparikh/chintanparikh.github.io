---
layout: post
title: "Is this how Tinder is going to monetize?"
date: 2013-07-20 00:28
comments: true
categories: 
---
So I'm at a Branch hackathon right now, and we're all just chilling. I decided to poke around Tinder and try to peek at their API.

Every second or so, there's a POST request to api.tinder.com/updates which passes in

```json
{
    "last_activity_date": "2013-07-20T02:57:36.127Z"
}
```

The response however, is a little more interesting:

```json
{
    "matches": [],
    "blocks": [],
    "matchmaker": [],
    "last_activity_date": "Sat, 20 Jul 2013 02:57:36 GMT",
    "trending": false
}
```

Matches and blocks are fairly obvious - new people you're matched with, and new people who have blocked you. However, it's the `trending` field that's a little more interesting. I'm completely spitballing here, but it's definitely possible that Tinder will charge users to "trend" to other users on tinder. Maybe this means that more people see them? I also have no idea what the `matchmaker` field is.

Any thoughts?

EDIT: I was using the Android version, so it didn't have the "matchmaker" feature. I just played with a friend's iOS phone, and it's pretty clear what the matchmaker attribute is.
