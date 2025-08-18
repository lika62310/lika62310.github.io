---
layout: default
title: Home
---

# Velkommen!

Alle indlæg:

{% for post in site.posts %}
- [{{ post.title }}]({{ post.url }}) — {{ post.date | date: "%B %d, %Y" }}
{% endfor %}
