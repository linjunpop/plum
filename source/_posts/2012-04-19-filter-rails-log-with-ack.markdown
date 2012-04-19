---
layout: post
title: "Filter rails log with ack"
date: 2012-04-19 08:31
comments: true
categories: [rails, shell]
---

Just a simple command to filter rails log with ack!

```bash
$ tail -F log/development.log | ack FOOBAR
```

