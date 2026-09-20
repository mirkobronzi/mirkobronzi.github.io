---
title: "Writing"
permalink: /posts/
layout: research
---

<header class="writing-header">
  <p class="eyebrow">Notes &amp; technical articles</p>
  <h1>Writing</h1>
  <p>Earlier writing on software engineering and machine learning tools, kept with its original publication dates. Technical instructions reflect the tools available at the time.</p>
</header>
<div class="writing-list">
  {% for post in site.posts %}
  <article class="writing-entry">
    <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: '%B %-d, %Y' }}</time>
    <h2><a href="{{ post.url | relative_url }}">{{ post.title | escape }}</a></h2>
    <p>{{ post.excerpt | strip_html | normalize_whitespace | truncatewords: 36 }}</p>
  </article>
  {% endfor %}
</div>
