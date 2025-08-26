---
layout: default
title: Projekt
---

<h1>Projekt Posts</h1>
<ul>
  {% for post in site.posts %}
    {% if post.tags contains "projekt" %}
       <li>
      <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
      <p><em>{{ post.date | date: "%B %d, %Y" }}</em></p>
      <div>{{ post.content }}</div>
    </li>
    {% endif %}
  {% endfor %}
</ul>
