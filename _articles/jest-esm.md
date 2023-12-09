---
topic: testing
title: Jest and ESM 
layout: default
published: yes 
---

# Jest, ESM and the long tail

I was quite surprised when belatedly installing jest to insert some unit tests before a refactoring effort to get this old favourite: 

{% highlight javascript %}
({"Object.<anonymous>":function(module,exports,require,__dirname,__filename, jest)    
{import  { testFunction } from './question-markdown-functions.js'
SyntaxError: Cannot use import statement outside a module
{% endhighlight %}

Aha! I thought, an easy fix - jest simply assumes all tests are cjs until forced otherwise - so I slapped an `mjs` on the end of the test filename and modified the `jest.config.json` to:

{% highlight json %}
"testMatch": ["**/__tests__/**/.*[jt]s?", "**/?*.(spec|test).(mjs|js|ts)"],
{% endhighlight %}

... but no dice. 

So I find [modules aren't natively supported by jest](https://jestjs.io/docs/ecmascript-modules). But they've been around for a _while_, right? But it turns out that overcoming the dependency building for a mocking framework is a somewhat intractable problem as the three-year [running github issue](https://github.com/jestjs/jest/issues/9430) attests to. 

The upshot is using the delightful-sounding `--experimental-vm-modules` ('experimental' and 'test framework' are two phrases I try not to combine) - [here's a good writeup](https://gist.github.com/danpetitt/37f5c966886f54e457ece4b08d66e404) and in my google journey, a [reddit thread](https://www.reddit.com/r/node/comments/xore64/change_my_mind_theres_no_actually_compelling/) questioning ESM in node at all. 

I'm not giving up my imports just yet. 