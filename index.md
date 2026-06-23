---
layout: default
title: about
---

# Elias Miguel Leal

<p>The first post breaks down the core idea of 4DFlowNet and presents findings of my implementation of the paper.</p>

<hr>

## latest posts

<div class="home-posts">
{% for post in site.posts %}
<article class="home-post">
  <time class="post-date" datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%b %-d, %Y" }}</time>
  <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
</article>
{% endfor %}
</div>
