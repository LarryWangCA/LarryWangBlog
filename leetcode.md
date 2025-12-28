---
layout: page
title: LeetCode周赛专区
permalink: /leetcode/
---

<ul>
  {%- assign lc_posts = site.posts | where_exp: "p", "p.categories contains '周赛'" -%}
  {%- for post in lc_posts -%}
    <li style="margin-bottom: 1rem;">
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      <span> — {{ post.date | date: "%Y-%m-%d" }}</span>

      {%- comment -%}
        提取文章中所有二级标题（## ...）并显示全部
        兼容 <h2 id="...">标题</h2>、</h2 >、以及内部带 <a> 的情况
      {%- endcomment -%}
      {%- assign html = post.content | markdownify -%}
      {%- assign parts = html | split: '<h2' -%}

      {%- if parts.size > 1 -%}
        <ul>
          {%- for part in parts offset:1 -%}
            {%- assign after_tag = part | split: '>' | slice: 1, 1 | join: '' -%}
            {%- assign h2_raw = after_tag | split: '</h2' | first -%}
            {%- assign h2_text = h2_raw | strip_html | split: '<' | first | strip -%}
            {%- if h2_text != '' -%}
              <li>{{ h2_text }}</li>
            {%- endif -%}
          {%- endfor -%}
        </ul>
      {%- endif -%}
    </li>
  {%- endfor -%}
</ul>
