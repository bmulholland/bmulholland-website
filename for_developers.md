---
layout: index
title: Resources for Developers
sidebar_link: true
sidebar_sort_order: 2
---

<h1>Resources for Developers</h1>
<ul>
  {% for resource in site.developer_resources %}
  <h3>
    <a href="{{ resource.url }}">
      {{ resource.title }}
    </a>
  </h3>
  {% endfor %}
</ul>
