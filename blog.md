---
layout: default
title: blog
permalink: /blog/
---

<div class="blog-index">
{% for post in site.posts %}
<article class="blog-preview">
  <h1><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h1>
  {% if post.description %}
    <p class="blog-description">{{ post.description }}</p>
  {% endif %}
  <p class="post-meta">
    {% if post.read_time %}{{ post.read_time }} <span>&middot;</span>{% endif %}
    <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%B %-d, %Y" }}</time>
  </p>
  {% if post.category %}
    <p class="post-category"><span aria-hidden="true">&#9632;</span> {{ post.category }}</p>
  {% endif %}
</article>
{% endfor %}
</div>
