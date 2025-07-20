---
layout: default
title: Publications
permalink: /publications/
---

<h2>Published Journal Articles</h2>
<ul>
{% assign pubs_sorted = site.publications | sort: "date" | reverse %}
{% for pub in pubs_sorted %}
  {% if pub.type == "journal-published" %}
    <li><a href="{{ pub.url }}">{{ pub.title }}</a> ({{ pub.journal }}, {{ pub.date | date: "%Y" }})</li>
  {% endif %}
{% endfor %}
</ul>

<h2>Submitted Journal Articles</h2>
<ul>
{% for pub in pubs_sorted %}
  {% if pub.type == "journal-submitted" %}
    <li><a href="{{ pub.url }}">{{ pub.title }}</a> ({{ pub.journal }}, {{ pub.date | date: "%Y" }})</li>
  {% endif %}
{% endfor %}
</ul>

<h2>Conference Papers</h2>
<ul>
{% for pub in pubs_sorted %}
  {% if pub.type == "conference" %}
    <li><a href="{{ pub.url }}">{{ pub.title }}</a> ({{ pub.journal }}, {{ pub.date | date: "%Y" }})</li>
  {% endif %}
{% endfor %}
</ul>
