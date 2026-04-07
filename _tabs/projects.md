---
layout: page
title: Projects
icon: fas fa-briefcase
order: 2
permalink: /projects/
---

This page showcases selected technical projects. Projects are sourced from `_data/projects.yml`. Each project may contain:

- `title` (string) — required
- `description` (string) — optional
- `url` (string) — optional, link to live demo
- `repo` (string) — optional, link to source repository
- `tech` (array) — optional, list of technologies
- `year` (number) — optional
- `featured` (boolean) — optional, when true the project is highlighted
- `order` (number) — optional, lower numbers display first

How it works
- Featured projects (where `featured: true`) are surfaced first and ordered by `order`.
- Remaining projects are shown afterward, ordered by `order`.


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

Example project YAML (put this in <code>_data/projects.yml</code>):

- title: "Personal Portfolio (This Site)"
  description: >
    A responsive personal portfolio and blog built with Jekyll and the Chirpy theme.
  url: "https://GargantuaM87.github.io"
  repo: "https://github.com/GargantuaM87/gargantuam87.github.io"
  tech:
    - Jekyll
    - Liquid
    - SCSS
  year: 2026
  featured: true
  order: 1


- title: "CLI Ops"
  description: "Cross-platform CLI automations for developer workflows."
  repo: "https://github.com/username/cli-ops"
  tech:
    - Node.js
    - TypeScript
  year: 2025
  featured: false
  order: 2


Notes and tips
- Note: image/thumbnail support has been removed from the Projects page; only textual project fields (title, description, tech, repo, year, featured) are used now.
- The page uses simple CSS classes (`projects-grid`, `project-card`, `project-thumb`, `project-body`, `project-title`, `project-description`, `project-meta`, `tech-badge`) so you can style them in your theme SCSS. If you want, I can add a small SCSS snippet that matches the Catppuccin Mocha palette and makes the project cards look polished.
- If you want pagination, filters by tech, or a different layout (carousel, masonry, etc.) I can implement that as a follow-up.