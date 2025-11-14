---
layout: page
title: 首页
permalink: /
---

# 欢迎来到我的博客 👋

这里是用 **GitHub Pages + Jekyll** 搭建的博客。

---

<ul>
  {%- assign essay_posts = site.posts | where_exp: "p", "p.categories contains '随笔'" -%}
  {%- for post in essay_posts -%}
    <li>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      <span> — {{ post.date | date: "%Y-%m-%d" }}</span>

      {%- comment -%} 提取第一个二级标题 ## ... {%- endcomment -%}
      {%- assign html = post.content | markdownify -%}
      {%- assign h2_parts = html | split: '<h2' -%}
      {%- if h2_parts.size > 1 -%}
        {%- assign after_tag = h2_parts[1] | split: '>' | slice: 1, 1 | join: '' -%}
        {%- assign first_h2 = after_tag | split: '</h2>' | first | strip | strip_html -%}
        {%- if first_h2 != '' -%}
          <br><strong>{{ first_h2 }}</strong>
        {%- endif -%}
      {%- endif -%}

    </li>
  {%- endfor -%}
</ul>

