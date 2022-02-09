---
title: "시각화"
layout: archive
permalink: categories/cs_basic
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories['Computer Science'] %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}