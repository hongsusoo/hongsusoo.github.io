---
title: "Python"
layout: archive
permalink: categories/ct_python
author_profile: true
sidebar_main: true
---


{% assign posts = site.categories['ct_python'] %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}