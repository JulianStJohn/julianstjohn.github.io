---
title: articles
layout: default
---

# Articles 

<ul>
  {% for article in site.articles %}
  {% if article.title != "Index" and article.title != "articles" %}
    <li>
      <h2><a href="{{ article.url }}">{{ article.title}}</a></h2>
    </li>

  {% endif%}
  {% endfor %}
</ul>