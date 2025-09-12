---
layout: default
title: Data science
---

<h1>Data Science</h1>
<ul>
  {% for post in site.posts %}
    {% if post.tags contains "data-science" %}
       <li>
      <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
      <p><em>{{ post.date | date: "%B %d, %Y" }}</em></p>
      <div>{{ post.content }}</div>
    </li>
    {% endif %}
  {% endfor %}
</ul>
