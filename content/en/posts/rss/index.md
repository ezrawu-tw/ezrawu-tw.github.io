---
slug: rss
copyright: true
title: "What is RSS? A Tool Everyone Should Know About"
date: 2026-05-07
updated:
tags:
categories:
  - Note
keywords:
description:
top_img:
cover:
---
slug: rss

# What's RSS
RSS stands for Really Simple Syndication.
In short, it extracts web content and turns it into an XML file, allowing users to subscribe to and read all their favorite sources in one place using an RSS Feed along with an RSS reader.

## Why RSS
RSS is an essential feature of every traditional blog. In the past, you could often spot a small icon that looked like a WiFi symbol tucked in a corner of websites.
Through this feature, people could stay updated on their favorite authors' new content — much like having a newspaper delivered — without having to visit each website individually.

Previously, gathering knowledge and news often required switching between different platforms:
Medium, websites or blogs, TV news, Facebook pages, Twitter... and so on.

Back when the internet was just getting started, this felt manageable. But as the age of information overload arrived, RSS began making a comeback.
This time, people use it not just as a simple subscription tool, but also as an essential remedy for shifting from passive to active reading.

## Passive Reading
With today's rapid technological advancement, AI and algorithms control the vast majority of what we see online.
As a result, we tend to see only the following types of content:

Sensational, violent, or gossip-driven content
Content the algorithm decides we'll like based on past behavior
Content advertisers want us to see

## Active Reading
Active reading means taking a stand against all of that and reclaiming your autonomy.
In the past, when we wanted to gain knowledge, we might have chosen books on specific topics.
But nowadays, what we need to choose is:
=> The right media sources

Whether it's YouTubers, news channels, personal blogs, or content platforms — it all counts.

Start actively building your own media diet.

## RSS reader
The devices we use most for reading are probably our phones or iPads.
Some well-known RSS readers include Feedly and Inoreader. Personally, I prefer Feedly for its layout and ease of use.

# Installation

> Referencing the official GitHub guide
https://github.com/hexojs/hexo-generator-feed

```
npm install hexo-generator-feed --save
```

Add the following code to the `_config.yml` file in your Hexo directory:

```
# RSS
# https://github.com/hexojs/hexo-generator-feed
feed:
  enable: true #whether to enable the plugin
  type: atom #options are atom and rss2; the default atom is fine
  path: atom.xml #the default atom.xml is also fine
  limit: 20 #number of posts to display; use 0 or false to show all
  hub: #not used here; leave blank as per the official docs
  content: #defaults to false; set to true to include full post content in the rss file
  content_limit: 140 #excerpt length
  content_limit_delim: ' ' #unclear from official docs; leaving as default
  order_by: -date #sort by date
  icon: icon.png #set an icon for the rss link
  autodiscovery: true #auto-discover feeds
  template: #configure a template for rss posts
```
