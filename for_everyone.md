---
layout: index
title: Resources for Everyone
sidebar_link: true
sidebar_sort_order: 1
---

<h1>Resources for Everyone</h1>
<ul>
  {% for resource in site.everyone_resources %}
  <h3>
    <a href="{{ resource.url }}">
      {{ resource.title }}
    </a>
  </h3>
  {% endfor %}
</ul>
