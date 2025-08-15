---
layout: default
title: Publications
permalink: /publications/
---

{% assign pubs_sorted = site.publications | sort: "date" | reverse %}

{% comment %}
Build filtered arrays so forloop.index counts within each group.
{% endcomment %}
{% assign journals_acc = pubs_sorted | where: "type", "journal" | where: "status", "accepted" %}
{% assign journals_sub = pubs_sorted | where: "type", "journal" | where: "status", "submitted" %}
{% assign conferences = pubs_sorted | where: "type", "conference" %}

<h1>Published Journal Articles</h1>
<ul>
  {% for pub in journals_acc %}
    <li>
      [J{{ forloop.index }}]
      <a href="{{ pub.url }}">{{ pub.title }}</a>
      {% if pub.journal %} ({{ pub.journal }}, {{ pub.date | date: "%Y" }}){% endif %}
    </li>
  {% endfor %}
</ul>

<h1>Submitted Journal Articles</h1>
<ul>
  {% for pub in journals_sub %}
    <li>
      <!-- Don’t number these with J#, since you only wanted accepted journals indexed -->
      <a href="{{ pub.url }}">{{ pub.title }}</a>
      {% if pub.journal %} ({{ pub.journal }}, {{ pub.date | date: "%Y" }}){% endif %}
    </li>
  {% endfor %}
</ul>

<h1>Conference Papers</h1>
<ul>
  {% for pub in conferences %}
    <li>
      [C{{ forloop.index }}]
      <a href="{{ pub.url }}">{{ pub.title }}</a>
      {% if pub.conference %} ({{ pub.conference }}, {{ pub.date | date: "%Y" }}){% endif %}
    </li>
  {% endfor %}
</ul>
