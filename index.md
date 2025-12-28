---
layout: page
title: Home
permalink: /
---

# Problems (by tag)

{% assign posts = site.tags.array | sort: "date" %}

<h2>array</h2>
<ul>
  {% for post in posts %}
    {%- assign html = post.content | markdownify -%}
    {%- assign parts = html | split: '<h2' -%}

    {%- if parts.size > 1 -%}
      {%- for part in parts offset:1 -%}
        {%- assign id_part = part | split: 'id="' -%}
        {%- assign h2_id = "" -%}
        {%- if id_part.size > 1 -%}
          {%- assign h2_id = id_part[1] | split: '"' | first -%}
        {%- endif -%}

        {%- assign after_tag = part | split: '>' | slice: 1, 1 | join: '' -%}
        {%- assign h2_raw = after_tag | split: '</h2' | first -%}
        {%- assign h2_text = h2_raw | strip_html | strip -%}

        {%- if h2_text contains "Leetcode" -%}
          <li>
            <a href="{{ post.url | relative_url }}{% if h2_id != '' %}#{{ h2_id }}{% endif %}">
              {{ h2_text }}
            </a>
          </li>
        {%- endif -%}
      {%- endfor -%}
    {%- endif -%}
  {% endfor %}
</ul>
