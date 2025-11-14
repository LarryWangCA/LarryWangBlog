---
layout: page
title: 首页
permalink: /
---

# 欢迎来到我的博客 👋

这里是用 **GitHub Pages + Jekyll** 搭建的博客。

[→ 查看「周赛」专页]({{ "/leetcode/" | relative_url }})

---

<ul>
  {%- assign essay_posts = site.posts | where_exp: "p", "p.categories contains '随笔'" -%}
  {%- for post in essay_posts -%}
    <li>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      <span> — {{ post.date | date: "%Y-%m-%d" }}</span>
      {%- if post.excerpt -%}<br>{{ post.excerpt | strip_html | truncate: 120 }}{%- endif -%}
    </li>
  {%- endfor -%}
</ul>

