---
layout: null
sitemap: false
---
<?xml version="1.0" encoding="UTF-8"?>
<rss version="2.0" xmlns:atom="http://www.w3.org/2005/Atom">
  <channel>
    <title>{{ site.title | xml_escape }}</title>
    <description>{{ site.description | xml_escape }}</description>
    <link href="{{ site.url }}{{ site.baseurl }}"</>
    <atom:link href="{{ "/rss/" | prepend: site.baseurl | prepend: site.url }}" rel="self" type="application/rss+xml" />
    {% for post in site.posts limit:10 %}
      <item>
        <title>{{ post.title | xml_escape }}</title>
        <description>{{ post.content | xml_escape }}</description>
        <pubDate>{{ post.date | date: "%a, %d %b %Y %H:%M:%S %z" }}</pubDate>
        <link rel="alternate" href="{{ post.url | prepend: site.baseurl | prepend: site.url }}" />
        <guid isPermaLink="true">{{ post.url | prepend: site.baseurl | prepend: site.url }}</guid>
      </item>
    {% endfor %}
  </channel>
</rss>
