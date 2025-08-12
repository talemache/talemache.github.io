
---
layout: page
title: Archive
permalink: /archive/
---

{% assign grouped = site.posts | group_by_exp:"post", "post.date | date: '%Y'" %}
{% for year in grouped %}
### {{ year.name }}
<ul>
  {% for post in year.items %}
    <li><a href="{{ post.url | relative_url }}">{{ post.title }}</a> <span style="color:#596070">— {{ post.date | date: "%b %d" }}</span></li>
  {% endfor %}
</ul>
{% endfor %}
