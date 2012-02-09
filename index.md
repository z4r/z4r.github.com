---
layout: page
title: Can I do this?
---
{% include JB/setup %}

![hate](/images/bookmark_wordle.png)

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

