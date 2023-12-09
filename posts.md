---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default 
title: posts
---


<ul>
  {% for post in site.posts %}
    <li>
        {%- assign date_format = site.minima.date_format | default: "%b %-d, %Y" -%}
      {{ post.date | date: date_format }} - <a href="{{ post.url }}">{{ post.title }}</a> 
    </li>
  {% endfor %}
</ul>