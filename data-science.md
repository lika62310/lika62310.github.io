---
layout: default
title: Data science
---

<h1>Data science</h1>
<ul>
  {% for post in site.posts %}
    {% if post.tags contains "data-science" %}
      <li><a href="{{ post.url }}">{{ post.title }}</a> - {{ post.date | date: "%B %d, %Y" }}
      
{{ post.content }}
</li>
    {% endif %}
  {% endfor %}
</ul>
