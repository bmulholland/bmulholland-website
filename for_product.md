---
layout: index
title: Resources for Product
sidebar_link: true
sidebar_sort_order: 3
---

<h1>Resources for Product</h1>
<ul>
  {% for resource in site.product_resources %}
  <h3>
    <a href="{{ resource.url }}">
      {{ resource.title }}
    </a>
  </h3>
  {% endfor %}
</ul>

