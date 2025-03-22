---
layout: post
title:  "RIP Chrome Custom Search Engines"
date:   2025-03-22 
categories: blog
---

For at least a decade I've been using a productivity hack that I thought I was _ingenious_ for discovering. Chrome allows ['Custom Search Engines'](chrome://settings/searchEngines), allowing you to open a website search page using a keyword and a search string - e.g. if your workflow system looks like,  `https://agile-workflow-board.com/stories/34555`  then a custom search engine of:
* Shortcut: `agilestories`
* URL: `https://agile-workflow-board.com/stories/%S`
 
will open the link typing `agilestories <TAB> 34555`  in the search bar. 

Pretty handy! But what if you just... ignored the search functionality used it as a link? 
* Shortcut: mylink
* URL: https://my-long-url.com

Well, then you'd have a set of universal persistant one word shortcut links synched to your chrome identity! And I have... a _lot_

![](/assets/images/search-engines.jpg)

I even had a _custom search engine link to the 'Custom Search Engines' interface_, I used it that much

![](/assets/images/heartbreak.jpg){: width="200"}{: style="float:right"}

Well as of last chrome build, that's all been removed. Links without %S won't work! I had thought losing my smart little hack was my own personal 💔, but looks like [plenty of people](https://support.google.com/chrome/thread/329004893/manage-search-engines-only-works-with-for-shortcuts-with-s-in-the-query?hl=en) were using the functionality in this way. 

If I had to guess, i would say this is a bug fix that has been in the Chrome backlog for an actual lifetime, and people like myself have been using it as an undocumented feature. 

It makes me think - however ingeniously you design, how rigorously you test - there is no replicating the ingenuity of the multitudes of users in breaking - or just enthusiastically using - your product. 