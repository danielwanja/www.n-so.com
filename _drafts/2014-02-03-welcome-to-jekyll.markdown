---
layout: post
title:  "Welcome to Jekyll!"
date: 2014-02-03 11:00
categories: jekyll update
comments: true
author: Daniel Wanja
image: 2014-02-03-wellcome-to-jekyll.jpg
---

Oops, I did it again. I'm talking about using a new blog engine. I started with Typo, migrated to several hosts over the years, used octopress, and now I moved straight to using [jekyll]http://jekyllrb.com. In this post I'll show you the behind the scenes and you will also find the source code of this site.


<!--more-->

This [github](https://github.com/danielwanja/www.n-so.com) repo is the CMS for my website and blog and is built using [jekyll](http://jekyllrb.com/).

I'm considering making the source of http://n-so.com website public. The content I create will be made available under the Creative Commons Attribution license.  Not being a designer I've started the site with an HTML template I bought, so please don't reuse the CSS and assets they provide unless you [buy the template](https://wrapbootstrap.com/theme/plixis-multipurpose-theme-WB0R03263).

My initial goal was to us [github page](http://pages.github.com/), a cool way to host your website. I'll blog about how I've create this site. If you can't wait, they are already many resources out there explaining how to use [jekyll](http://jekyllrb.com/). However I'm also using custom plugin to allow using layouts in HAML which github pages doesn't allow for obvious security reasons. Let me know if you find out otherwise. S3 was the next contender for hosting this site and with the [s3_website](https://github.com/laurilehmijoki/s3_website) gem it's even more convenient than gh-pages.

Enjoy!
\- Daniel Wanja


* Explain why jekyll
* Explain where hosted (and why not github pages)
* What no AngularJS yet? Will move it to plain AngularJS removing all jQuery
* Bought and customize template. You'll need to buy it if you want to reuse this code.
*

You'll find this post in your `_posts` directory - edit this post and re-build (or run with the `-w` switch) to see your changes!
To add new posts, simply add a file in the `_posts` directory that follows the convention: YYYY-MM-DD-name-of-post.ext.

Jekyll also offers powerful support for code snippets:


{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out the [Jekyll docs][jekyll] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll's GitHub repo][jekyll-gh].

[jekyll-gh]: https://github.com/mojombo/jekyll
[jekyll]:    http://jekyllrb.com
