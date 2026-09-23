---
layout: page
title: Curriculum
subtitle: Required knowledge from the welcome letter — each stop has its own notes page.
permalink: /curriculum/
---

<div class="prose">
  <p>Basic history of Aarhus / Denmark, plus the stops below. ARoS and Moesgaard are introduce-only (not guided). The Old Town is an exam.</p>
  <p class="note-callout">You will be able to do walking tours in different variations (exam), and 1 or 2 bus tours with visits in different variations.</p>
</div>

{% assign foundation = site.data.program.places | where: "scope", "foundation" %}
{% assign guide = site.data.program.places | where: "scope", "guide" %}
{% assign introduce = site.data.program.places | where: "scope", "introduce" %}
{% assign exam = site.data.program.places | where: "scope", "exam" %}

<section class="section">
  <h2>Foundation</h2>
  <ul class="place-list">
    {% for p in foundation %}
    <li>
      <a href="{{ '/places/' | append: p.slug | append: '/' | relative_url }}">
        {{ p.title }}
        <span class="hint">{{ p.scope_label }}</span>
      </a>
    </li>
    {% endfor %}
  </ul>
</section>

<section class="section">
  <h2>Guide stops</h2>
  <ul class="place-list">
    {% for p in guide %}
    <li>
      <a href="{{ '/places/' | append: p.slug | append: '/' | relative_url }}">
        {{ p.title }}
        <span class="hint">{{ p.scope_label }}</span>
      </a>
    </li>
    {% endfor %}
  </ul>
</section>

<section class="section">
  <h2>Introduce only</h2>
  <ul class="place-list">
    {% for p in introduce %}
    <li>
      <a href="{{ '/places/' | append: p.slug | append: '/' | relative_url }}">
        {{ p.title }}
        <span class="hint">{{ p.subtitle | default: p.scope_label }}</span>
      </a>
    </li>
    {% endfor %}
  </ul>
</section>

<section class="section">
  <h2>Exam</h2>
  <ul class="place-list">
    {% for p in exam %}
    <li>
      <a href="{{ '/places/' | append: p.slug | append: '/' | relative_url }}">
        {{ p.title }}
        <span class="hint">{{ p.subtitle | default: p.scope_label }}</span>
      </a>
    </li>
    {% endfor %}
  </ul>
</section>
