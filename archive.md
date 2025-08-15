---
layout: page
title: 
permalink: /archive/
---

<div class="archive-list">
{% assign grouped = site.posts | group_by_exp:"post", "post.date | date: '%Y'" %}
{% for year in grouped %}
### {{ year.name }}
<ul>
  {% for post in year.items %}
    <li>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a> 
      <span style="color: var(--muted-color)">— {{ post.date | date: "%b %d" }}</span>
    </li>
  {% endfor %}
</ul>
{% endfor %}
</div>