---
layout: post
title: "Automated Visual regression of mobile apps using nakal"
description: ""
category: automation
tags: []
---
{% include JB/setup %}

In mobile apps market, looks of an application is extremely important. With long running projects, any minor
refactoring can change your app's looks.
While we have functional testing tools like appium and calabash, its equally important to have some test coverage
 around looks of your app. And, with nakal gem we can automate the visual testing of ios and android.

## Installation

Add this line to your application's Gemfile:

    gem 'nakal'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install nakal

## Usage

If you are using cucumber, include following Lines in your env.rb

	require "nakal/cucumber"
	Nakal.platform = :android

	for ios, set:

	Nakal.platform = :ios


and then put this line in your automation code, at all places where a new screen loads:

	diff = nakal_execute("current_screen_name")

Now, execute your test by passing env variable NAKAL_MODE=build to build the baseline images

once baseline is built, next execution onwards, start using environment variable NAKAL_MODE=compare to compare against baseline.
any difference will be put in the same directory with image file named "current_screen_name_diff.png"


For setting custom directory, use:

	Nakal.directory= "<desired_directory>"
	Nakal.device_name = "nexus7"

For cropping the notification bar OR scroll bar, create a config/nakal.yml file in execution directory

eg:

put these contents in your nakal.yml file inside config/nakal.yml

	samsung_galaxy_s3:
	 top: 50
	 right: 18
	 left: 0
	 bottom: 0

	nexus7:
	 top: 74
	 right: 20
	 left: 0
	 bottom: 0

	iPhone_5s:
	 top: 30
	 right: 6
	 left: 0
	 bottom: 0