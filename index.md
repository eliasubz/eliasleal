---
layout: about
title: about
---

# Elias Miguel Leal

<p> Master Student at Universitat Politècnica de Catalunya and doing a thesis in action anticipation from egocentric video. </p> 

<hr>

## Blog

<div class="home-posts">
{% for post in site.posts %}
<article class="home-post">
  
  <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
  <!-- add unterschrift  -->
  <!-- below write the expected reading time and date on one line but make it gray and not too big -->
  <!-- <time class="post-date" datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%b %-d, %Y" }}</time> -->
</article>
{% endfor %}
</div>
