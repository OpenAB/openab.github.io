---
title: Archive
layout: default
---

# News Archive

<div class="post-nav-container">
  {% if site.posts.size > 0 %}
  <nav class="post-nav">
    <ul>
      {% for post in site.posts %}
      <li class="{% if url == post.url %}active{% endif %}">    
        <a href="{{post.url}}" title="{{post.title}}">
          <span>{{post.title}}</span>
          {{post.date | date: '%d %B %Y'}}
        </a>
      </li>
      {% endfor %}
    </ul>
  </nav>
  {% else %}
  <p>
    Sorry, there are currently no posts to display.
  </p>
  {% endif %}
</div>
