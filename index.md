---
layout: default
title: Home
---

<section class="hero">
  <p class="eyebrow">Nordic Guide Academy · Aarhus</p>
  <h1>Class notes for NGA Aarhus 2026</h1>
  <p class="lede">Notes from the Nordic Guide Academy Aarhus 2026 course — by session and place, with original source material kept alongside.</p>
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

<section class="section" id="coming-up" hidden>
  <h2>Coming up</h2>
  <ul class="session-list" id="coming-up-list"></ul>
</section>

<script type="application/json" id="program-sessions">
[
{% assign all = site.data.program.fall | concat: site.data.program.spring %}
{% for s in all %}
  {
    "date": {{ s.date | jsonify }},
    "date_label": {{ s.date_label | jsonify }},
    "starts": {{ s.starts | default: "00:00" | jsonify }},
    "ends": {{ s.ends | default: "23:59" | jsonify }},
    "title": {{ s.title | jsonify }},
    "where": {{ s.where | jsonify }},
    "teachers": {{ s.teachers | jsonify }},
    "url": {{ '/sessions/' | append: s.slug | append: '/' | relative_url | jsonify }}
  }{% unless forloop.last %},{% endunless %}
{% endfor %}
]
</script>
<script>
(function () {
  var section = document.getElementById("coming-up");
  var list = document.getElementById("coming-up-list");
  var dataEl = document.getElementById("program-sessions");
  if (!section || !list || !dataEl) return;

  var sessions;
  try {
    sessions = JSON.parse(dataEl.textContent);
  } catch (e) {
    return;
  }

  function copenhagenStamp(date) {
    var parts = {};
    new Intl.DateTimeFormat("en-GB", {
      timeZone: "Europe/Copenhagen",
      year: "numeric",
      month: "2-digit",
      day: "2-digit",
      hour: "2-digit",
      minute: "2-digit",
      hour12: false
    }).formatToParts(date).forEach(function (p) {
      if (p.type !== "literal") parts[p.type] = p.value;
    });
    // en-GB may use 24:00 for midnight; normalise hour
    var hour = parts.hour === "24" ? "00" : parts.hour;
    return parts.year + "-" + parts.month + "-" + parts.day + "T" + hour + ":" + parts.minute;
  }

  function sessionStamp(s, time) {
    return s.date + "T" + (time || "00:00");
  }

  var now = copenhagenStamp(new Date());

  var upcoming = sessions
    .filter(function (s) {
      return s.date && sessionStamp(s, s.ends || "23:59") > now;
    })
    .sort(function (a, b) {
      var aStart = sessionStamp(a, a.starts || "00:00");
      var bStart = sessionStamp(b, b.starts || "00:00");
      return aStart < bStart ? -1 : aStart > bStart ? 1 : 0;
    })
    .slice(0, 3);

  if (!upcoming.length) return;

  upcoming.forEach(function (s) {
    var li = document.createElement("li");
    var a = document.createElement("a");
    a.href = s.url;

    var date = document.createElement("span");
    date.className = "date";
    date.textContent = s.date_label;

    var body = document.createElement("span");
    var title = document.createElement("strong");
    title.textContent = s.title;
    body.appendChild(title);

    var sub = document.createElement("div");
    sub.className = "sub";
    sub.textContent = [s.where, s.teachers].filter(Boolean).join(" · ");
    body.appendChild(sub);

    a.appendChild(date);
    a.appendChild(body);
    li.appendChild(a);
    list.appendChild(li);
  });

  section.hidden = false;
})();
</script>
