---
layout: page
title: Trantect
tagline: Agile software development for the future world
---

  {% for post in site.posts %}
## <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a>

<p>

  <small><span id="date">{{ post.date | date_to_string }}</span>
  In:  
  {% for category in post.categories %}   
  <a href="categories.html" class="category_link">
  {{ category }} 
  </a>
  {% endfor %}
  </small>
</p>
  



<p>
  {{ post.content}}
</p>

  {% endfor %}




