---
title: '{{ replace .File.ContentBaseName "-" " " | title }}'
# URL slug = bundle folder name (matches notebooks/<slug>.ipynb)
slug: '{{ .ContentBaseName }}'
subtitle: ''
date: '{{ .Date }}'
draft: true
keywords: ''
tags: []
# Optional — uncomment and set repo:
# notebook_url: "https://github.com/USER/REPO/blob/main/notebooks/{{ .ContentBaseName }}.ipynb"
---
