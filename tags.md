---
layout: page
title: View Tags
---

<div class="tags-expo-list">
    {% for tag in site.tags %}
    <a href="#{{ tag[0] | slugify }}" class="post-tag">{{ tag[0] }}</a>
    {% endfor %}
  </div>
 
  <div class="related">
    {% for tag in site.tags %}
    <h2 id="{{ tag[0] | slugify }}">{{ tag[0] }}</h2>
    <ul class="related-posts">
      {% for post in tag[1] %}
        <a class='p-link' href="{{ post.url }}">
      <li>
        {{ post.title }}
      <small>{{ post.date | date_to_string }}</small>
      </li>
      </a>
      {% endfor %}
    </ul>
    {% endfor %}
  </div>