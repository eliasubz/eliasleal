---
layout: about
title: about
---

# Elias Miguel Leal

<p> Master Student at Universitat Politècnica de Cataluny, currently working on a thesis in struggle anticipation from egocentric video. </p> 

<hr>

## Blog

<div class="home-posts">
{% for post in site.posts %}
<article class="home-post">
  <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
  <time class="post-date" datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%b %-d, %Y" }}</time>
</article>
{% endfor %}
</div>
