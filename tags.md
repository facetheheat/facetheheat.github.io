---
layout: page
title: Тэги
sitemap: false
---

{% capture site_tags %}{% for tag in site.tags %}{{ tag | first }}{% unless forloop.last %},{% endunless %}{% endfor %}{% endcapture %}
<!-- site_tags: {{ site_tags }} -->
{% assign tag_words = site_tags | split:',' | sort %}
<!-- tag_words: {{ tag_words }} -->

<div id="tags">
  {% for item in (0..site.tags.size) %}
    {% unless forloop.last %}
      {% capture this_word %}{{ tag_words[item] | strip_newlines }}{% endcapture %}
        <h3 id="{{ this_word | cgi_escape }}">{{ this_word }}</h3>
        <ul class="posts">
        {% for post in site.tags[this_word] %}
          {% if post.title != null %}
            <li><small>{{ post.date | date: site.date_format }}</small> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
          {% endif %}
        {% endfor %}
        </ul>
    {% endunless %}
  {% endfor %}
</div>
