---
layout: page
title: Articles
description: "Technical articles on .NET, Python, AI, cybersecurity, and developer tools."
---

<input type="text" id="search-box" placeholder="🔎 Search articles..." class="search-box">

<div class="article-grid" id="articles-list">
  {% for post in site.posts %}
  <article class="article-card" dir="{{ post.direction | default: 'ltr' }}" data-title="{{ post.title | downcase }}">
    
    {% if post.categories.first %}
    <span class="article-card__category">{{ post.categories.first }}</span>
    {% endif %}

    <h3 class="article-card__title">
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
    </h3>

    <p class="article-card__excerpt">
      {{ post.excerpt | strip_html | truncatewords: 25 }}
    </p>

    <div class="article-card__meta">
      <time datetime="{{ post.date | date_to_xmlschema }}">
        {{ post.date | date: "%B %d, %Y" }}
      </time>

      <a href="{{ post.url | relative_url }}" class="article-card__link">
        Read more →
      </a>
    </div>

  </article>
  {% endfor %}
</div>

<script>
document.getElementById("search-box").addEventListener("keyup", function() {

  let filter = this.value.toLowerCase();
  let items = document.querySelectorAll("#articles-list .article-card");

  items.forEach(function(item){

    let title = item.getAttribute("data-title");

    if(title.includes(filter)){
      item.style.display = "block";
    } else {
      item.style.display = "none";
    }

  });

});
</script>