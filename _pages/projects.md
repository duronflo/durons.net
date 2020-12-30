---
layout: collection
author_profile: true
title: Übersicht Projekte
permalink: /projects/
---

<ul>
  {% for project in site.projects %}
      <h1><a href="{{ project.url }}">{{ project.title }} </a> </h1>

      <strong> Kurzbeschreibung:</strong> {{ project.short_description }}
      <p><p>
      <strong> Projekt-Status:</strong> <i>: {{ project.status }}</i>


      <p class="page__date">
      <strong><i class="fas fa-fw fa-calendar-alt" aria-hidden="true"></i> Projekt-Beginn:</strong> 
      <i>: {{ project.project_start }}</i>
      </p>

      <p class="page__taxonomy">
        <strong><i class="fas fa-fw fa-folder-open" aria-hidden="true"></i> {{ site.data.ui-text[site.locale].categories_label | default: "Categories:" }} </strong>
        <span itemprop="keywords">
           {% for category in project.categories %}
                <a href="{{ site.url }}/categories/#{{ category }}" class="page__taxonomy-item" rel="tag">{{ category }}</a> 
          {% endfor %}
        </span>
      </p>

      <p class="page__taxonomy">
        <strong><i class="fas fa-fw fa-tags" aria-hidden="true"></i> {{ site.data.ui-text[site.locale].tags_label | default: "Tags:" }} </strong>
        <span itemprop="keywords">
            {% for tag in project.tags %}
                 <a href="{{ site.url }}/tags/#{{ tag }}" class="page__taxonomy-item" rel="tag">{{ tag }}</a> 
           {% endfor %}  
        </span>
      </p>
   
      
    <p><p><p>

  {% endfor %}
</ul>