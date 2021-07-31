---
title: "Grammar"
layout: archive
permalink: categories/py_grammar
author_profile: true
sidebar_main: true
---


{% assign posts = site.categories["py_grammar"] %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}