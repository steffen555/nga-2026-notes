---
layout: page
title: Sources
subtitle: Original notes and handouts as received, with who provided them.
permalink: /sources/
---

{% assign published_sources = site.sources | where_exp: "s", "s.published != false" %}

{% if published_sources.size == 0 %}
<p class="empty">No source material yet.</p>
{% else %}
<ul class="source-list">
  {% for src in published_sources %}
  <li>
    <a href="{{ src.url | relative_url }}">
      <strong>{{ src.title }}</strong>
      <span class="sub">
        {{ src.author }}
        {% if src.author_role %} · {{ src.author_role }}{% endif %}
        · {{ src.format_label | default: src.format }}
        · received {{ src.received }}
      </span>
    </a>
  </li>
  {% endfor %}
</ul>
{% endif %}
