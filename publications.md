---
layout: default
title: Publications
permalink: /publications/
---

{% comment %}
Build filtered arrays in chronological order (oldest → newest).
We'll display them with `reversed` (newest first), but compute numbers so oldest = 1.
{% endcomment %}
{% assign journals_acc = site.publications | where: "type", "journal" | where: "status", "accepted" | sort: "date" %}
{% assign journals_sub = site.publications | where: "type", "journal" | where: "status", "submitted" | sort: "date" %}
{% assign conferences = site.publications | where: "type", "conference" | sort: "date" %}

<h1>Published Journal Articles</h1>
<ul>
  {% for pub in journals_acc reversed %}
    {% assign jid = forloop.length | minus: forloop.index | plus: 1 %}
    <li>
      [J{{ jid }}]
      <a href="{{ pub.url }}">{{ pub.title }}</a>
      {% if pub.journal %} ({{ pub.journal }}, {{ pub.date | date: "%Y" }}){% endif %}
    </li>
  {% endfor %}
</ul>

<h1>Submitted Journal Articles</h1>
<ul>
  {% for pub in journals_sub reversed %}
    <li>
      <!-- No numbering for submitted -->
      <a href="{{ pub.url }}">{{ pub.title }}</a>
      {% if pub.journal %} ({{ pub.journal }}, {{ pub.date | date: "%Y" }}){% endif %}
    </li>
  {% endfor %}
</ul>

<h1>Conference Papers</h1>
<ul>
  {% for pub in conferences reversed %}
    {% assign cid = forloop.length | minus: forloop.index | plus: 1 %}
    <li>
      [C{{ cid }}]
      <a href="{{ pub.url }}">{{ pub.title }}</a>
      {% if pub.conference %} ({{ pub.conference }}, {{ pub.date | date: "%Y" }}){% endif %}
    </li>
  {% endfor %}
</ul>
