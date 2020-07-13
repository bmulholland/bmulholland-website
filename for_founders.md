---
layout: index
title: Resources for Founders
sidebar_link: true
sidebar_sort_order: 4
---

<h1>Resources for Founders</h1>
<ul>
  {% for resource in site.founder_resources %}
  <h3>
    <a href="{{ resource.url }}">
      {{ resource.title }}
    </a>
  </h3>
  {% endfor %}
</ul>

