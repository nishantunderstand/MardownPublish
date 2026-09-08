---
layout: default
title: "Nishant's Blog"
---

# Nishant's Blog

Welcome to my technical blog.

## Latest Articles

{% for post in site.posts %}
### [{{ post.title }}]({{ post.url | relative_url }})

{{ post.excerpt }}

[Read more →]({{ post.url | relative_url }})

---
{% endfor %}