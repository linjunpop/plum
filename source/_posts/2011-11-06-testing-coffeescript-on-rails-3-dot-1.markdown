---
layout: post
title: "Testing CoffeeScript on Rails 3.1"
date: 2011-11-06 10:11
comments: true
categories: [rails, coffeescript, testing, rspec]
---

## install the gems
- - -

		group :development, :test do
			gem 'jasminerice'
			gem 'guard'
			gem 'guard-rspec'
			gem 'guard-jasmine'
			# for mac
			gem 'rb-fsevent', :require => false
			gem 'growl_notify', :require => false # or gem 'growl'
			# for linux
			gem 'rb-inotify', :require => false
			gem 'libnotify', :require => false
		end
		
## Init
- - -

Add guard definition to your `Guardfile` by running this command:

		$ guard init jasmine

and add a route for the Jasmine Test Runner to `config/routes.rb`:

		if ["development", "test"].include? Rails.env
		  mount Jasminerice::Engine => "/jasmine"
		end

Next you create the directory `spec/javascripts` where your CoffeeScript tests go into. You define the Rails 3.1 asset pipeline manifest in `spec/javascripts/spec.js.coffee`:

		#=require_tree ./
		
## Install `phantomjs` (headless WebKit with JavaScript API)
- - -

With `Homebrew` on Mac OS X and install it with:

		$ brew install phantomjs
		
for Ubuntu, you can install it with apt:

		$ sudo add-apt-repository ppa:jerome-etienne/neoip
		$ sudo apt-get update
		$ sudo apt-get install phantomjs

## Run the test
- - -

run the following command on your terminal, and you will see the result.

		$ guard
		
## refs
- - -

[https://github.com/netzpirat/guard-jasmine](https://github.com/netzpirat/guard-jasmine)

[https://github.com/bradphelan/jasminerice](https://github.com/bradphelan/jasminerice)

[http://code.google.com/p/phantomjs/](http://code.google.com/p/phantomjs/)

[https://github.com/guard/guard](https://github.com/guard/guard)
