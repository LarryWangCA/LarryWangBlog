---
layout: page
title: 代码训练营一刷笔记
permalink: /
---

# Welcome 👋

---
layout: page
title: Home
permalink: /
---

# Welcome 👋

- [Day1–Day60（First Pass）](/day1-60/)
- [Weekly / Biweekly Contests](/leetcode/)

---

## Browse by Category (Tags)

{% assign groups = "array,hash-table,linked-list,string,stack-queue,tree,backtracking,greedy,dp,monotonic-stack,heap,bit,math,graph" | split: "," %}

{% for tag in groups %}
  {% assign posts = site.tags[tag] %}
  {% if posts and posts.size > 0 %}
  <h2>{{ tag }}</h2>
  <ul>
    {% for post in posts %}
      <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
        <span> — {{ post.date | date: "%Y-%m-%d" }}</span>
      </li>
    {% endfor %}
  </ul>
  {% endif %}
{% endfor %}
