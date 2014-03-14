# Welcome to www.n-so.com

An AngularJS and Ruby on Rails agency. This github repo is the CMS for my website and blog.

I'm considering making the source of http://n-so.com website public. The content I create will be made available under the Creative Commons Attribution license.  Not being a designer I've started the site with an HTML template I bought, so please don't reuse the CSS and assets they provide unless you [buy the template](https://wrapbootstrap.com/theme/plixis-multipurpose-theme-WB0R03263).

Now github provides [github page](http://pages.github.com/), a cool way to host your website which is what I've decided to go with. I'll blog about how I've create this site. If you can't wait, they are aleady many resources out there explaining how to use it. But in short, check out the [gh-pages](https://github.com/danielwanja/www.n-so.com/tree/gh-pages) branch of this repo.

I want to use HAML for my layouts and this currently is not supported by github pages. Let me know if you find out otherwise. The implications are the automated Jekyll generation on github doesn't work. So the Master branch now contains all the main code for the site, generating the output to the _site folder. That output get's checked into the *gh-pages* repo which is then served statically without Jekyll processing from github pages.

Enjoy!
\- Daniel Wanja

[@danielwanja](http://twitter.com/danielwanja)
