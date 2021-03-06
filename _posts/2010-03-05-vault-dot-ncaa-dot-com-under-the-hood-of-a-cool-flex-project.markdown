---
layout: post
title: "vault.ncaa.com : under the hood of a cool Flex project."
date: 2010-03-05 19:10
comments: true
categories: flex
---

<div style="text-align:center;"><img src="http://onrails.org/files/vault.png" alt="vault.png" border="0" width="350" height="378" /></div>

<a href="http://www.thoughtequity.com">Thought Equity Motion</a> and <a href="http://www.ncaa.com/">NCAA</a> two days ago officially released the <a href="http://vault.ncaa.com/">Ncaa Vault</a>. A cool Flex app backed by an incredible video database with awesome metedata about each game...and released just in time for March Madness.

Here are a few of the announcements and online articles describing the services:

<!--more-->

* <a href="http://fs.ncaa.org/Docs/PressArchive/2010/20100303+thought+equity+march+madness+rls.htm">NCAA and Thought Equity Motion Unveil First Ever Video-Powered Vault for NCAA March Madness</a> - by NCAA
* <a href="http://www.nytimes.com/2010/03/03/sports/ncaabasketball/03ncaa.html">N.C.A.A. Tournament Goes Online, Clip by Clip</a> - by the New York Times
* <a href="http://www.wired.com/playbook/2010/03/say-hello-to-the-ncaa-vault-adieu-to-productivity/#ixzz0hGq1bpTzhttp://www.wired.com/playbook/2010/03/say-hello-to-the-ncaa-vault-adieu-to-productivity/">Say Hello to NCAA Vault, Adieu to Productivity</a> - by Wired

In fact with the Vault you can have a URL right into a specific moment of any game and Wired picked out a great <a href="http://bit.ly/c9eQSU">last second tying shot</a>.

The twittersphere feedback is also <a href="http://search.twitter.com/search?q=vault+ncaa">pretty impressive</a>.

This is the most visible Flex app I worked on :-) Late January <a href="http://twitter.com/theaboutbox">Cameron Pope</a> contacted me to ask if I could help on a Flex project for NCAA and Thought Equity. The funny part is that I didn't know that Cameron was such a great Flex developer, I met him via the Denver Ruby on Rails User Group (derailed) and I also didn't know what NCAA was (don't shoot, I didn't grow up in the US and we don't have TV). So when I asked my father in law about NCAA and realized it was about Basketball I was intrigued by what type of application we needed to build. Cameron showed me the mockups built by Donny Wells which is just an awesome graphical designer. These mockups where just incredible and then I was presented the video service technology the Thought Equity Motion team put together, and I was just blown away and though that this would be a cool project to work on.

Cameron was the main Flex developer and I just worked part time on Monday's on this project. If you need and incredible Flex developer just contact Cameron.

Now let's dive more into the Flex nitty-gritty details:

For the mvc architecture  we used the <a href="http://swizframework.org/">Swiz Framework</a> and this turned out to  work exceptionally well. Swiz sports some dependency injection features that can be enabled via the [Autowire] tag and I was surprised when I realized I could also just use that feature in an item render. Let's look at a little detail...For the play by play timeline if a play is in the future it is displayed in bold:

<div style="text-align:center;"><img src="http://onrails.org/files/timeline.png" alt="timeline.png" border="0" width="350" height="129" /></div>

So each line of the timelime is rendered by the TimeLineItemRender and you can just autowire the model which contains the playhead position.

<pre>
      [Autowire]
      [Bindable]
      public var vaultModel:Vault;
</pre>

The we can set the style name accordingly based on the play's start time and the current playhead position:

<pre>
   styleName="{data.startTime < vaultModel.playheadPosition ? 'past' : 'future'}"
</pre>

The style of the application was created by the designer and Cameron did a great job reproducing it using <a href="http://www.degrafa.org/">Degrapha</a> for skinning () using an approach similar to this <a href="http://www.degrafa.org/source/ButtonLoader/ButtonLoader.html">example</a> (example <a href="http://www.degrafa.org/source/ButtonLoader/srcview/index.html">source</a>)

Most of my work was around the searching, bug fixing and general architecture overview. We took a similar approach to the one I described <a href="http://onrails.org/articles/2007/11/27/flash-utils-bytearray-compressing-4-1mb-to-20k">here</a> in order to avoid most of the server round trips during searching.

The Flex app is just a pretty face,  behind the scene Thought Equity provides an incredible services that they will expose in many ways, the start can be seen <a href="http://www.thoughtequity.com/video/home/article/ncaa_vault_publishing.do">here</a> and all that data will be able to be accessed via API and other means.

This was a short but incredible project for me, the guys at Though Equity have such an incredible vision on how to turn these sport videos into something so much bigger! Thank you guys for getting me on board.

<div style="text-align:center;"><img src="http://onrails.org/files/thoughtequity.png" alt="thoughtequity.png" border="0" width="245" height="30" /></div>

Enjoy!
Daniel Wanja
