---
layout: default
title: blog
permalink: /blog/
---

# blog

{% for post in site.posts %}
<article class="post-list-item">
  <time class="post-date" datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%b %-d, %Y" }}</time>
  <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
  {% if post.description %}
    <p>{{ post.description }}</p>
  {% endif %}
</article>
{% endfor %}
