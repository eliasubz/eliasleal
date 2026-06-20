---
layout: default
title: blog
permalink: /blog/
---

# blog

{% for post in site.posts %}
<div class="post-list-item">
  <span class="post-date">{{ post.date | date: "%b %-d, %Y" }}</span>
  <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
  {% if post.description %}
    <p>{{ post.description }}</p>
  {% endif %}
</div>
{% endfor %}
