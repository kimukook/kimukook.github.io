---
layout: default
title: Projects
permalink: /projects/
---

<h1>Projects</h1>

<p>Below are some of the research projects I’ve been working on. Each project showcases multiple efforts and publications on a shared theme.</p>

<ul>
  {% for project in site.projects %}
    {% if project.category == "main" %}
      <li>
        <h3><a href="{{ project.url }}">{{ project.title }}</a></h3>
        {% if project.summary %}
          <p>{{ project.summary }}</p>
        {% endif %}
      </li>
    {% endif %}
  {% endfor %}
</ul>
