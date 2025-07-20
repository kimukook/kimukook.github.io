---
layout: default
title: Publications
permalink: /pubs/
---

<h1>Publications</h1>
<ul>
  {% for pub in site.publications %}
    <li><a href="{{ pub.url }}">{{ pub.title }}</a> ({{ pub.journal }})</li>
  {% endfor %}
</ul>
