---
layout: default
permalink: /notes/
title: notes
description: short notes to myself and to whoever stumbles across them
---

<div class="post">

<h1>notes</h1>
<p class="post-metadata">{{ page.description }}</p>

{% comment %}
Collect the tags and categories actually used by the notes collection, so this
page links only to note archives. Tag/category archives for notes are
namespaced under /notes/ (see jekyll-archives in _config.yml), so they can
never collide with the blog's /blog/tag/ pages.

The `post` layout renders note tags as plain text rather than links (it only
links tags for /blog/ URLs), so the two blocks below are what make the
/notes/tag/ and /notes/category/ archive pages reachable.
{% endcomment %}
{% assign note_tag_list = "" | split: "" %}
{% assign note_category_list = "" | split: "" %}
{% for note in site.notes %}
{% for tag in note.tags %}
    {% assign note_tag_list = note_tag_list | push: tag %}
{% endfor %}
{% for category in note.categories %}
    {% assign note_category_list = note_category_list | push: category %}
{% endfor %}
{% endfor %}
{% assign note_tags = note_tag_list | uniq | sort %}
{% assign note_categories = note_category_list | uniq | sort %}

{% if note_tags.size > 0 %}
  <h4>tags</h4>
  <div class="tag-category-list">
    <ul class="p-0 m-0">
      {% for tag in note_tags %}
        <li>
          <i class="fa-solid fa-hashtag fa-sm"></i>
          <a href="{{ tag | slugify | prepend: '/notes/tag/' | relative_url }}">{{ tag }}</a>
        </li>
        {% unless forloop.last %}
          <p>&bull;</p>
        {% endunless %}
      {% endfor %}
    </ul>
  </div>
{% endif %}

{% if note_categories.size > 0 %}
  <h4>categories</h4>
  <div class="tag-category-list">
    <ul class="p-0 m-0">
      {% for category in note_categories %}
        <li>
          <i class="fa-solid fa-tag fa-sm"></i>
          <a href="{{ category | slugify | prepend: '/notes/category/' | relative_url }}">{{ category }}</a>
        </li>
        {% unless forloop.last %}
          <p>&bull;</p>
        {% endunless %}
      {% endfor %}
    </ul>
  </div>
{% endif %}

<ul class="posts">
  {% assign notes = site.notes | sort: 'date' | reverse %}
  {% for note in notes %}
    <li>
      <span class="post-meta">
        <a href="{{ note.date | date: '/notes/%Y/' | relative_url }}">{{ note.date | date: '%b %d, %Y' }}</a>
      </span>
      <h3 class="post-title">
        <a href="{{ note.url | relative_url }}">{{ note.title }}</a>
      </h3>
      {% if note.description %}
        <p class="post-description">{{ note.description }}</p>
      {% endif %}
    </li>
  {% endfor %}
</ul>

</div>
