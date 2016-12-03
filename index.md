---
layout: default
---

<div class="posts">
  {% assign posts = (site.posts | where: "lang", site.active_lang) %}
  {% for post in posts  %}
    <article class="post">

      <h1><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h1>

      <div class="entry">
        {{ post.excerpt }}
      </div>

      <a href="{{ site.baseurl }}{{ post.url }}" class="read-more">{{site.ReadMore[site.active_lang]}}</a>
    </article>
  {% endfor %}
</div>
