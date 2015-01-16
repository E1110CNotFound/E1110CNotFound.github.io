---
layout: page
title: 最近更新
---
{% include JB/setup %}

<ul class="posts">
  {% for post in site.posts %}
    <li>
      <span class="post-meta">{{ post.date | date: "%b %-d, %Y" }} • {% if post.categories %}{% for category in post.categories %} {{ category }}{% endfor %}{% endif %}</span>

      <h2>
        <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
      </h2>
    </li>
  {% endfor %}
</ul>