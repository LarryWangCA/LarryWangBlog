---
layout: page
title: Home
permalink: /
---

# Problems Index (by Tag)

{% assign groups = "array,dp,tree,bit,heap,greedy,backtracking,string,hash-table,linked-list,stack-queue,monotonic-stack,math,graph" | split: "," %}

{% for tag in groups %}
  {% assign posts = site.tags[tag] %}
  {% if posts and posts.size > 0 %}
    {% assign posts = posts | sort: "date" %}

    <h2>{{ tag }}</h2>
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

            {%- assign gt = part | split: '>' -%}
            {%- assign after_tag = gt[1] -%}
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

  {% endif %}
{% endfor %}
