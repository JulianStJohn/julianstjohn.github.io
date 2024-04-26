---
topic: playwright
title: Playwright Tips 
layout: default
published: yes 
---

# Playwright tips

Playwright is an excellent asynchronous UI-level browser testing tool, with its own test framework. It can have you up and runnning with browser and API tests extremely quickly, and is built to effortlessly handle the challenges of modern web framework testing. 

Here's a few tips I've gleaned as I've used it. 


## Finding an element's parent 

Playwright has a definite design philosophy: tests should manipulate user-facing elements. I would guess this is an attempt to stamp out brittle and ugly xpaths of the `//div[@class='mainContent']/div/div[2]/ul/ul[2]` variety, preferencing self-explaining function chains. Contrasting with every other browser testing tool I've used, there isn't an `element` at all - the class has been removed from the playwright API. 

Each `locator` method in playwright returns a carved-out chunk of the DOM, be it one tag, a tag containing other tags, or an array of either. So where in javascript it's trivial to find an element's parent (e.g. `document.getElementById('answer-item).parentElement`), playwright has no `parentElement` property because there _is no parent element_ to the part of the DOM returned by the `locator`.

Instead, the `has` filter allows you to search for the parent directly, so for the HTML hierachy: 

```html
<div id='answer'>
  <div class='row active' role='row'>
    <span class='question-number-column'>34</span>
    <span class='answer-column'>1886</span>
    <span class='explanation-column'>First coca-cola sale.</span>
```

If we were interested in retrieving the value of `span.answer-column` for the question number 34, we might first look for the row:

```javascript
const answerRow = page.locator(page.getByRole('row'), { has: page.locator("span.question-number-column").filter({hasText: "34"})});
```
and then find the child element we are after:

```javascript
const answer = answerRow.locator("span.answer-column").innerText();
```


## Navigating Shadow DOMs

[Shadow DOMs](https://developer.mozilla.org/en-US/docs/Web/API/Web_components/Using_shadow_DOM) have been adding degrees of difficulty to UI testing for over a decade now. If you haven't come across the concept, Shadow DOMs allow web components to be individually styled without the styles affecting the rest of the page. You could consider the Shadow DOM root to be like a reference to a separate HTML page:

```html
<div id='chatBot container'>
  #shadow-root (open)
  <div id='menu-row'>
```

As they are references rather than attached to the DOM, XPath selectors will not traverse Shadow DOMS - the contents are entirely invisible to XPath selectors.  However, css selectors _will_, and, mercifully, playwright locators [work with a Shadow DOMs](https://playwright.dev/docs/locators#locate-in-shadow-dom) out of the box. The exception is, of course, locators using Xpath.

If you do _really_ want to use an XPath locator _within_ a Shadow DOM, you'll need to base the XPath locator on a non-XPath locator that selects items in the Shadow DOM: 

```javascript
page.locator("div#menu-row").locator("//div[contains(@class, 'menu-item')])
```




