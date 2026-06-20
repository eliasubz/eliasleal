---
layout: default
title: about
---

# Flow MRI Notes

This is a small research blog about recreating 4D flow MRI papers with cheap, inspectable experiments.

The first post rebuilds the core idea of 4DFlowNet: map low-resolution noisy 3D velocity fields to super-resolved velocity fields, then evaluate whether the model preserves quantities that matter for hemodynamics.

---

## latest posts

{% for post in site.posts %}
{{ post.date | date: "%b %-d, %Y" }} [{{ post.title }}]({{ post.url | relative_url }})
{% endfor %}
