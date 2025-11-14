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

      {%- capture first_h2 -%}
        {{ post.content | markdownify | split: '<h2>' | slice: 1, 1 | join: '' | split: '</h2>' | first | strip }}
      {%- endcapture -%}
      {%- if first_h2 != '' -%}
        <br><strong>{{ first_h2 }}</strong>
      {%- endif -%}

    </li>
  {%- endfor -%}
</ul>

