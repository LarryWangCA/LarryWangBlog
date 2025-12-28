
---
layout: page
title: Home
permalink: /
---

# Browse by Tag → Problems

{% assign groups = "array,dp,tree,bit,heap,greedy,backtracking,string,hash-table,linked-list,stack-queue,monotonic-stack,math,graph,contest" | split: "," %}

{% for tag in groups %}
  {% assign posts = site.tags[tag] %}
  {% if posts and posts.size > 0 %}

  <h2>{{ tag }}</h2>
  <ul>
    {% for post in posts %}
      {%- assign html = post.content | markdownify -%}
      {%- assign parts = html | split: '<h2' -%}

      {%- if parts.size > 1 -%}
        {%- for part in parts offset:1 -%}
          {%- comment -%}
            1) 抽取 h2 的 id
          {%- endcomment -%}
          {%- assign id_part = part | split: 'id="' -%}
          {%- if id_part.size > 1 -%}
            {%- assign h2_id = id_part[1] | split: '"' | first -%}
          {%- else -%}
            {%- assign h2_id = "" -%}
          {%- endif -%}

          {%- comment -%}
            2) 抽取 h2 的文字
          {%- endcomment -%}
          {%- assign after_tag = part | split: '>' | slice: 1, 1 | join: '' -%}
          {%- assign h2_raw = after_tag | split: '</h2' | first -%}
          {%- assign h2_text = h2_raw | strip_html | strip -%}

          {%- comment -%}
            3) 只显示包含 Leetcode 的标题（即题目）
          {%- endcomment -%}
          {%- if h2_text contains "Leetcode" -%}
            <li>
              <a href="{{ post.url | relative_url }}{% if h2_id != '' %}#{{ h2_id }}{% endif %}">
                {{ h2_text }}
              </a>
              <span style="opacity:0.7;">（来自：{{ post.title }}）</span>
            </li>
          {%- endif -%}
        {%- endfor -%}
      {%- endif -%}

    {% endfor %}
  </ul>

  {% endif %}
{% endfor %}
