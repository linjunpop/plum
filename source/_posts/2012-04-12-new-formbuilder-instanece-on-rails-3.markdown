---
layout: post
title: "Create a new FormBuilder instanece on Rails 3"
date: 2012-04-12 14:28
comments: true
categories: [rails]
---

As on rails 2 we can create a new `ActionView::Helpers::FormBuilder`
instance with

```Ruby
ActionView::Helpers::FormBuilder.new(:foobar, @foobar, @template, {}, proc{})
```

But on rails 3 this becomes

```Ruby
ActionView::Helpers::FormBuilder.new(:foobar, @foobar, this, {}, proc{})
```

Just take a note.

