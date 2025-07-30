---
layout: default
title: Projects
permalink: /projects/
---

<h1>Projects</h1>

<p>Below are some of the research projects I’ve been working on. Each project showcases multiple efforts and publications on a shared theme.</p>

<ul style="list-style-type: none; padding: 0;">
  {% for project in site.projects %}
    {% if project.category == "main" %}
      <li>
        <div class="project-block">
          <div class="project-media">
            {% if project.media %}
              {% if project.media contains '.mp4' %}
                <video autoplay muted loop playsinline width="300">
                  <source src="{{ project.media }}" type="video/mp4">
                  Your browser does not support the video tag.
                </video>
              {% else %}
                <img src="{{ project.media }}" alt="Project media" width="300" />
              {% endif %}
            {% endif %}
          </div>

          <div class="project-text">
            <h3><a href="{{ project.url }}">{{ project.title }}</a></h3>
            {% if project.summary %}
              <p class="project-summary">{{ project.summary }}</p>
            {% endif %}
          </div>
        </div>
      </li>
    {% endif %}
  {% endfor %}
</ul>


