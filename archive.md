---
layout: page
title: Архив
permalink: /archive/
---
<ul>
  {% for post in site.posts %}
    {% unless post.next %}
      <h3>{{ post.date | date: '%Y' }}</h3>
    {% else %}
      {% capture year %}{{ post.date | date: '%Y' }}{% endcapture %}
      {% capture nyear %}{{ post.next.date | date: '%Y' }}{% endcapture %}
      {% if year != nyear %}
        <h3>{{ post.date | date: '%Y' }}</h3>
      {% endif %}
    {% endunless %}

    	&emsp; {{ post.date | date:"%d/%m" }} <a href="{{ post.url }}">{{ post.title }}</a> <br>

  {% endfor %}
</ul>


