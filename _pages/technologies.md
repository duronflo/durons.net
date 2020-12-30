---
layout: collection
author_profile: true
title: Übersicht Technologien
permalink: /technologies/
---

<ul>
  {% for technology in site.technologies %}
      <h1><a href="{{ technology.url }}">{{ technology.title }} </a> </h1>

      <strong> Kurzbeschreibung:</strong> {{ technology.short_description }}
      <p><p>
 
      <p class="page__taxonomy">
        <strong><i class="fas fa-fw fa-folder-open" aria-hidden="true"></i> {{ site.data.ui-text[site.locale].categories_label | default: "Categories:" }} </strong>
        <span itemprop="keywords">
           {% for category in technology.categories %}
                <a href="{{ site.url }}/categories/#{{ category }}" class="page__taxonomy-item" rel="tag">{{ category }}</a> 
          {% endfor %}
        </span>
      </p>

      <p class="page__taxonomy">
        <strong><i class="fas fa-fw fa-tags" aria-hidden="true"></i> {{ site.data.ui-text[site.locale].tags_label | default: "Tags:" }} </strong>
        <span itemprop="keywords">
            {% for tag in technology.tags %}
                 <a href="{{ site.url }}/tags/#{{ tag }}" class="page__taxonomy-item" rel="tag">{{ tag }}</a> 
           {% endfor %}  
        </span>
      </p>
   
      
    <p><p><p>

  {% endfor %}
</ul>