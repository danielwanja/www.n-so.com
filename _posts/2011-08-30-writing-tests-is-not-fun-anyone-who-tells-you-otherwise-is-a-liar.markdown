---
layout: post
title: "Writing tests is not fun. Anyone who tells you otherwise is a liar...."
date: 2011-08-30 20:03
comments: true
categories:
---
At least so says my good friend Sean Voisen in his latest blog entry <a href="http://sean.voisen.org/blog/2011/08/thoughts-on-test-driven-development">Thoughts on test-driven development</a>.

What, you are calling me a liar? :-) I must respectfully disagree with Sean. Not on the fact that he may think it's not fun, that's his opinion like many other Flex developers that don't do testing. I disagree because I see many developers, in other communities, that actually really enjoy testing. If you look at the Ruby community you will see many developpers enjoying doing test driven development, enjoying writing tests, and even expanding the way you can write tests. Check out rspec, Cucumber, and the many of books and screencast on the subject. Checkout all the ruby libraries, they are all pretty well tested. There are many training classes on people that really want to improve doing testing. Many Rails projects are extremly well tested. Many Ruby developers cannot even code without writing tests first.

<!--more-->

This said as they are many examples on how to test Ruby and Rails code it's easier to get going on with testing in that environment. On the other hand, there are not many example of tested Flex applications and libraries. Not many toturoials on how to test your Flex application.
I happend to do a lot of unit testing for my Flex apps, but I do not test everything, I use tests for more difficult aspects, when I'm not sure how to design something, when it's slow to access a part of the application just to verify that my new code works. Then I write tests and it's fun. How many times do you manually repeat a sequence on the UI like start the application, perform a search, click on the grid, open a record, click the calculate button...Oh no, that not right...go change some code and do it again. Well that's not fun. Every developer I know does that thousands a time a day. Well, write a test and your workflow becomes more fun.

So why are Flex developers not testing? As I mentioned above, there is not much peer pressure to do so as not many Flex developers do testing. Also they are not many examples. In addition it's not obvious how to test applications in many case. Often they are not written in a testable manner. Flex/ActionScript is asynchronous and event driven, that's harder too.

They are solutions for that and Flex applications are very well suited to testing...but the sweet spot must be found. And you should start by testing the simple things that have lots of added value. Anywhere you have logic in your code that does filtering, calculation, transform data, write a test...You gonna like it. FlexUnit 4 as great support for asynchronous or event driven programming, but I agree, at first it's not obvious how to best us that support. So again, start with the simple thing, refactor your code so that you can test it in a non-asynchronous way, that will already be helpfull.

So I came to the conclusion that I won't be able to convince Flex developers that testing is needed and even fun. I can only hope that as a Flex developer you will start using FlexUnit 4 and try to add tests to your application and persevere and find the sweet spot on where testing is fun and makes you more productive. If you persevere you will like many Ruby developers become a better developer, write better code and faster.

I finally like Sean's balanced view on test driven development: "But would I use TDD for every project I work on? Probably not. For personal â€œone-offâ€ projects or projects I know will not see much future maintenance, the slower development time is simply not worth it. For serious, long-term projects however, TDD is now a must."

Testing remains hard, but it's just essential if you want to become a great, agile, developer.

Persevere and testing will become your friend!

Enjoy!
Daniel

