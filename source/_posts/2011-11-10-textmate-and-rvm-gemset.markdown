---
layout: post
title: "TextMate and RVM Gemset"
date: 2011-11-10 10:41
comments: true
categories: [textmate, rvm, gemset]
---

Navigate to `Preferences` -> `Advanced` -> `Shell Variables`, add followed variables:

```
TM_RUBY: /Users/Jun/.rvm/bin/rvm-auto-ruby
GEM_HOME: env | grep GEM_HOME | awk '{ sub(/GEM_HOME=/, ""); print }'
GEM_PATH: env | grep GEM_PATH | awk '{ sub(/GEM_PATH=/, ""); print }'
```