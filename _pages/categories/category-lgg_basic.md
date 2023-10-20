---
title: "Basic"
layout: archive
permalink: categories/py_basic
author_profile: true
sidebar_main: true
---


{% assign posts = site.categories['Python Basic'] %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}