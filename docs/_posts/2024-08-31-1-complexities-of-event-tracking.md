---
layout: post
title: Complexities of Event Tracking
date: 2024-08-31 15:30:00 +0800
categories: []
---

For the most of us working on customer facing products, there is always a strong need to track events as they help us understand the users' behavior and then utilize the information to further improve upon our product. There are many platforms in the market like Google Analytics, Mixpanel and many others but they all come with jarring one issue - over time, it can get very tedious to understand all the available events flowing thru the system and if they are correctly implemented. Ultimately many of companies still resort to very traditional excel or google sheets to list down all the events. Some of the key challenges I have found using this method are as follows:
1. A level of overlapping/duplicate work in terms of maintaining events
2. Inconsistent/insufficient documentation specifics around what fields are required, and what they should be named
3. Difficult to validate/verify events that have been created in production and hence a lack of confidence if the events are implemented the right way

Interestingly, I stumbled upon a solution called [avo](https://www.avo.app/), which solves many of the challenges that I have seen, and possibly a bit more