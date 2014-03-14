---
layout: post
title: "Using Jasminerice to test CoffeeScript in a Rails Engine"
date: 2012-09-08 20:20
comments: true
categories: rails
---

[Jasmine](http://pivotal.github.com/jasmine/) is a behavior-driven development framework for testing JavaScript and CoffeeScript code. I wanted to use it to test CoffeeScript for a Rails Engine I am working on. Enters 
[Jasminerice](https://github.com/bradphelan/jasminerice) a gem that let's you add Jasmine tests to your Rails application. From it's website Jasminerice takes "full advantage of the Rails 3.1 asset pipeline. Jasminerice removes any excuse YOU have for not testing your out of control sprawl of CoffeeScript files.".  This said out of the box the Jasminerice  gem does not support Rails Engines. It's a Rails Engine itself, but from their website [they say](https://github.com/bradphelan/jasminerice/issues/40) "Unfortunately this is currently not working when used in a mountable engine.".

So I looked under the hood of the gem and found that with a couple of fixes you can get it working with a Rails Engine.

<!--more-->

Ideally I will create a pull request and have Jasminerice work for plain Rails apps and for Rails Engine. For now you can follow these instructions to get it working with your Engine. Please let me know if you find a nicer/simpler way to test your Rails Engines with Jasmine.

The main difference is that in a Rails Engine all your Rails classes and Java/CoffeeScript are namespaced and you need to tell Jasminerice to look in a few different places.

###### Enabling Jasminerice for you engines

So with a simple initialization change of your application you can start using Jasminerice to test your engine!


In your spec/dummy/config/routes.rb add the following to mount Jasminerice

```ruby
  if Rails.env.test? || Rails.env.development?
    mount Jasminerice::Engine => "/jasmine"
    get "/jasmine/:suite" => "jasminerice/spec#index"
  end
```

Then create the following initializer in config/initializers/jasminerice.rb

```ruby
if Rails.env.test? || Rails.env.development?
    Rails.application.config.assets.paths << OnlineAudit::Engine.root.join("spec", "javascripts") << OnlineAudit::Engine.root.join("spec", "stylesheets")
    # Add engine to view path so that spec/javascripts/fixtures are accessible
    ActionController::Base.prepend_view_path OnlineAudit::Engine.root  
end
```

This tells jasmine to find your specs in  spec/javascript folder (and not in spec/dummy/spec) and where to find the jasmine fixture files (in spec/javascript/fixtures).

Of course don't forget to add the gem "jasminerice"   to the development and test group of your Gemfile.

###### Using Jasminerice

Create these two support files to let jasmine load css and javascript files:  

spec/javascripts/spec.css

```
/*
 *= require application
 */
```

spec/javascripts/spec.js.coffee

```
#= require jquery
#= require jquery_ujs
#= require jquery.ui.all
#= require_tree . 
jasmine.getFixtures().fixturesPath = 'fixtures'
```

To use fixture you need to tell the javascript part of Jasmine where to find the fixtures. That path is wrong by default when testing a Rails Engine.

Then write a spec i.e. spec/javascripts/add_remove_controller_spec.js.coffee

```
#= require my_engine/my_controller

describe "AddRemoveController", ->
  it "exists", ->
    expect(1).toEqual(1)
    expect(MyEngine.MyController).not.toBeUndefined()

  it "has html", ->
    loadFixtures "an_html_file"
    addButton = $('article#subcontractors .add_fields')
    expect(addButton).not.toBeUndefined()
```

Note the loadFixtures loads an html file from the spec/javascripts/fixtures folder. In the above spec we use jQuery to find some elements in that HTML document. Also note that when you require the coffeescript file you want to test, here the my_controller.js.coffee, you must specify your engine path my_engine/ in this case.


To view the results of all your tests:
http://localhost:3000/jasmine


A few good resources to learn more about jasmine:

- [http://pivotal.github.com/jasmine](http://pivotal.github.com/jasmine)
- [http://railscasts.com/episodes/261-testing-javascript-with-jasmine-revised](http://railscasts.com/episodes/261-testing-javascript-with-jasmine-revised)

<br/>
Happy testing!

- Daniel