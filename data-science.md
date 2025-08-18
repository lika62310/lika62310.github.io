---
layout: default
title: Data science
---

Data sciencePosts</h1>
<ul>
  {% for post in site.posts %}
    {% if post.tags contains "data-science" %}
      <li><a href="{{ post.url }}">{{ post.title }}</a> - {{ post.date | date: "%B %d, %Y" }}</li>
    {% endif %}
  {% endfor %}
</ul>
