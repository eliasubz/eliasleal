---
layout: default
title: about
---

# **Elias** Leal Spohr  

This is my personal website where I'm planning to publish blogs about my learning. 
{: .lede}

The first post breaks down the core idea of 4DFlowNet and presents findings of my implementatio of the paper. 
---

## latest posts

{% for post in site.posts %}
<article class="post-list-item">
  <time class="post-date" datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%b %-d, %Y" }}</time>
  <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
  {% if post.description %}
    <p>{{ post.description }}</p>
  {% endif %}
</article>
{% endfor %}
