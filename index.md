---
layout: default
title: Home
---

# Welcome to My Site

Here are my posts:

{% for post in site.posts %}
- [{{ post.title }}]({{ post.url }}) — {{ post.date | date: "%B %d, %Y" }}
{% endfor %}
