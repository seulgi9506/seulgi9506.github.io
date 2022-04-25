---
title: "Mini Todo"
layout: archive
permalink: categories/minitodo
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.minitodo %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}
