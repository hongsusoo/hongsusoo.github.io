---
title: "project angleprice"
layout: archive
permalink: categories/py_proj1
author_profile: true
sidebar_main: true
---


{% assign posts = site.categories['py_proj1'] %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}