---
title: "특강"
layout: archive
permalink: /categories/lectures
---

{% assign posts = site.categories.lectures %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}