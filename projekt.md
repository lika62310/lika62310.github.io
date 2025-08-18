---
layout: default
title: Projekt
---

<h1>Projekt Posts</h1>
<ul>
  {% for post in site.posts %}
    {% if post.tags contains "projekt" %}
      <li><a href="{{ post.url }}">{{ post.title }}</a> - {{ post.date | date: "%B %d, %Y" }}</li>
    {% endif %}
  {% endfor %}
</ul>
