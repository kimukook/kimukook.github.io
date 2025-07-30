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
        <div class="project-block">
          {% if project.media %}
            {% if project.media contains '.mp4' %}
              <video controls width="400" style="margin-bottom: 0.5em;">
                <source src="{{ project.media }}" type="video/mp4">
                Your browser does not support the video tag.
              </video>
            {% else %}
              <img src="{{ project.media }}" alt="Project media" style="width: 400px; margin-bottom: 0.5em;" />
            {% endif %}
          {% endif %}

          <h3><a href="{{ project.url }}">{{ project.title }}</a></h3>

          {% if project.summary %}
            <p style="color: gray; font-style: italic;">{{ project.summary }}</p>
          {% endif %}
        </div>
      </li>
    {% endif %}
  {% endfor %}
</ul>

