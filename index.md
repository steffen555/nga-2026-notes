---
layout: default
title: Home
---

<section class="hero">
  <p class="eyebrow">Nordic Guide Academy · Aarhus</p>
  <h1>Class notes for NGA Aarhus 2026</h1>
  <p class="lede">Notes from the Nordic Guide Academy Aarhus 2026 course — by session and place, with original source material kept alongside.</p>
  <div class="cta-row">
    <a class="btn" href="{{ '/program/' | relative_url }}">Program</a>
    <a class="btn btn-ghost" href="{{ '/sources/' | relative_url }}">Sources</a>
  </div>
</section>

<section class="section">
  <h2>Browse</h2>
  <div class="grid-cards">
    <a class="card-link" href="{{ '/program/' | relative_url }}">
      <strong>Program</strong>
      <span>Schedule and notes for each lesson, tour, and exam.</span>
    </a>
    <a class="card-link" href="{{ '/curriculum/' | relative_url }}">
      <strong>Curriculum</strong>
      <span>Stops and places for walking tours and exams.</span>
    </a>
    <a class="card-link" href="{{ '/sources/' | relative_url }}">
      <strong>Sources</strong>
      <span>Original notes and handouts as received.</span>
    </a>
    <a class="card-link" href="{{ '/practical/' | relative_url }}">
      <strong>Practical</strong>
      <span>Course tips, groups, and contacts.</span>
    </a>
  </div>
</section>

<section class="section">
  <h2>Course snapshot</h2>
  <div class="panel">
    <ul>
      <li>Wednesdays <strong>16.30–20.00</strong>, plus about one Saturday a month</li>
      <li>Usual classroom: <strong>Gelinde, Balticagade</strong> — always check the program</li>
      <li>At least <strong>80% attendance</strong> and contribution to <strong>guide gold</strong> for exams and diploma</li>
      <li>Goal: universal guide skills, basic Aarhus walking tours, and a few bus tours</li>
    </ul>
  </div>
</section>

<section class="section">
  <h2>Coming up</h2>
  <ul class="session-list">
    {% assign upcoming = site.data.program.fall | where_exp: "s", "s.number <= 3" %}
    {% for s in upcoming %}
    <li>
      <a href="{{ '/sessions/' | append: s.slug | append: '/' | relative_url }}">
        <span class="date">{{ s.date_label }}</span>
        <span>
          <strong>{{ s.title }}</strong>
          <div class="sub">{{ s.where }} · {{ s.teachers }}</div>
        </span>
      </a>
    </li>
    {% endfor %}
  </ul>
</section>
