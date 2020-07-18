---
layout: page
title: Books
permalink: /books/
---

This is my recommended list of books to read:

<ul class="posts">
{% for book in site.data.books %}
  <li class="posts-home-summary">
    <h2 class="post-title">{{ book.title }}</h2>

    <div class="post-meta">
       {{ book.author}}
    </div>
    <div class="post">
    {{ book.notes}}
    </div>
    <img src="{{ book.thumbnail }}" />
  </li>
{% endfor %}
</ul>