---
layout: page
permalink: /teaching/
title: teaching
description: Courses, syllabi, slides, and related teaching materials.
nav: true
nav_order: 6
---

<div class="teaching-page-intro">
  This page lists courses and seminars in a database-style format. Each row links to core materials such as syllabi, slide decks, assignments, datasets, and related student research topics.
</div>

<div class="teaching-db-toolbar">
  <input type="text" id="teaching-search" placeholder="Search course title, term, level, institution, tags">
  <select id="teaching-level">
    <option value="">All levels</option>
    <option value="Undergraduate">Undergraduate</option>
    <option value="Seminar">Seminar</option>
    <option value="Graduate">Graduate</option>
  </select>
</div>

<div class="teaching-db-wrap">
  <table class="teaching-db" id="teaching-db">
    <thead>
      <tr>
        <th>Course</th>
        <th>Term</th>
        <th>Level</th>
        <th>Institution</th>
        <th>Materials</th>
        <th>Status</th>
      </tr>
    </thead>
    <tbody>
      {% assign courses = site.data.courses | sort: "term" | reverse %}
      {% for course in courses %}
      <tr
        data-level="{{ course.level }}"
        data-search="{{ course.title | downcase }} {{ course.term | downcase }} {{ course.level | downcase }} {{ course.institution | downcase }} {{ course.tags | join: ' ' | downcase }}"
        id="{{ course.course_slug }}"
      >
        <td class="course-col">
          <div class="course-title">{{ course.title }}</div>
          {% if course.summary %}
          <div class="course-summary">{{ course.summary }}</div>
          {% endif %}
        </td>

        <td>{{ course.term }}</td>
        <td>{{ course.level }}</td>
        <td>{{ course.institution }}</td>

        <td class="materials-col">
          {% if course.syllabus %}
            <a href="{{ course.syllabus | relative_url }}">syllabus</a>
          {% endif %}
          {% if course.slides %}
            · <a href="{{ course.slides | relative_url }}">slides</a>
          {% endif %}
          {% if course.assignments %}
            · <a href="{{ course.assignments | relative_url }}">assignments</a>
          {% endif %}
          {% if course.datasets %}
            · <a href="{{ course.datasets | relative_url }}">datasets</a>
          {% endif %}
          {% if course.research %}
            · <a href="{{ course.research | relative_url }}">research topics</a>
          {% endif %}
        </td>

        <td>
          <span class="status-pill status-{{ course.status | downcase | replace: ' ', '-' }}">
            {{ course.status }}
          </span>
        </td>
      </tr>
      {% endfor %}
    </tbody>
  </table>
</div>

<script>
document.addEventListener("DOMContentLoaded", function () {
  const searchInput = document.getElementById("teaching-search");
  const levelSelect = document.getElementById("teaching-level");
  const rows = Array.from(document.querySelectorAll("#teaching-db tbody tr"));

  function applyFilters() {
    const q = (searchInput.value || "").toLowerCase().trim();
    const level = levelSelect.value;

    rows.forEach((row) => {
      const text = row.dataset.search || "";
      const rowLevel = row.dataset.level || "";

      const matchesSearch = !q || text.includes(q);
      const matchesLevel = !level || rowLevel === level;

      row.style.display = matchesSearch && matchesLevel ? "" : "none";
    });
  }

  searchInput.addEventListener("input", applyFilters);
  levelSelect.addEventListener("change", applyFilters);
  applyFilters();
});
</script>
