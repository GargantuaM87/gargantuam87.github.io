---
layout: page
title: Projects
icon: fas fa-briefcase
order: 2
permalink: /projects/
---


{% comment %}
Prepare two lists:
- featured_projects: projects with featured: true
- other_projects: all others
Use where and where_exp for filtering, then sort by `order` if present.
{% endcomment %}

{% assign featured_projects = site.data.projects | where: "featured", true | sort: "order" %}
{% assign other_projects = site.data.projects | where_exp: "p", "p.featured != true" | sort: "order" %}

{% assign projects = featured_projects | concat: other_projects %}

{% if projects and projects.size > 0 %}
<div class="projects-grid">
  {% for project in projects %}
  <article class="project-card {% if project.featured %}featured{% endif %}">
    <div class="project-row">
      <!-- Image support removed: project details render without thumbnails -->

      <div class="project-body">
        <h3 class="project-title">
          {% if project.url %}
            <a href="{{ project.url | relative_url }}" target="_blank" rel="noopener noreferrer">{{ project.title }}</a>
          {% else %}
            {{ project.title }}
          {% endif %}
        </h3>

        {% if project.description %}
          <p class="project-description">{{ project.description }}</p>
        {% endif %}

        <p class="project-meta">
          {% if project.tech %}
            <strong>Tech:</strong>
            {% for t in project.tech %}
              <span class="tech-badge">{{ t }}</span>{% unless forloop.last %},{% endunless %}
            {% endfor %}
          {% endif %}

          {% if project.repo %}
            {% if project.tech %} • {% endif %}
            <a href="{{ project.repo }}" target="_blank" rel="noopener noreferrer">Repository</a>
          {% endif %}

          {% if project.year %}
            {% if project.repo or project.tech %} • {% endif %}
            {{ project.year }}
          {% endif %}
        </p>
      </div>
    </div>
  </article>
  {% endfor %}
</div>
{% else %}
<p>No projects found. Create a file at <code>_data/projects.yml</code> and add your project entries. See the example below.</p>
{% endif %}

---
# Future Projects...
- Definately a Physics engine
- An old abandoned game that I've been meaning to finish 
- A game engine made in Vulkan, but that's after I grasp most of OpenGL
