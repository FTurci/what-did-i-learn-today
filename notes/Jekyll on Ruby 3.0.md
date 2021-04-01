---
title: Jekyll on Ruby 3.0
created: '2021-03-24T14:42:20.160Z'
modified: '2021-03-24T14:44:13.051Z'
---

# Jekyll on Ruby 3.0

An error may occurr when running 

```
bundle exec jekyll serve
```

on Ruby 3.0.0. 

To solve it, run

```
bundle add webrick
```
