---
layout: post
title: "iPhone App: Mi-Fi 1.2 now with iOS 4.x support. A must have if you have an Mifi card."
date: 2010-10-13 00:28
comments: true
categories: mobile ios
---

<div style="float:left; padding: 15px;">
<img src="http://www.onrails.org/files/mifi12.jpg" alt="mifi12.jpg" border="0" height="250" align="left" />
<a href="http://itunes.apple.com/app/mi-fi/id333601535?mt=8">
<img src="http://www.onrails.org/files/marketing_badge.png" alt="marketing_badge.png" border="0" width="121" height="61" align="left" />
</a>
</div>

I created the MiFi app during the 360iDev conference on September 29th 2009 and submitted the app the same day. I released a fix a month later and didn't touch the application since. I wasn't using my Mifi card much until recently when I realized that the app wasn't working on iOS 4.1. Then I checked the comments for the Mi-Fi app on the AppStore and realized that there where hundreds of comments of people that have the same issue. Sorry for being so late to realize that. Once I found that out I had to decide wether to remove the application from the store or fix it. So I reopened the project and realized that the way it was written wouldn't work in the new Titanium SDK. Despite of the work I decided to rewrite/reorganized the code and voilaâ€¦Mi-Fi 1.2 for iOS 4.1 should now work better than ever. I did not restyle the application, it could look better but it's still functional. I also  didn't add any feature but at least you should get the battery and reception levels that are the most important features. Another feature I should add soon is to be able to set the ip address of your Mi-Fi card in case you changed from the default address. 

<!--more-->

What is stranger to me is how many people downloaded the application, knowing that it didn't work on iOS4. About 400 downloads a weekâ€¦man.. many people must be wondering what this application does and in fact did, as the reviews show. Well, that should be fixed. Sorry for the delay!  Here is the weekly sales trend:

<br/>
<div style="text-align:center;"><img src="http://www.onrails.org/files/20101012MiFiWeeklySales.png" alt="20101012MiFiWeeklySales.png" border="0" width="450" /></div>

I also saw someone created  a $2.99 version of the same app called MyMiFi it does the same thing but it has a nicer design I would say. Maybe I should give "paid" a try and will release this one for $.99 centsâ€¦.or should I? The fact is that I really don't care about selling 10 apps or even 100 apps at $.99â€¦I maybe wouldn't say the say if I sold 1000â€¦So free it stays.

Now internally I had to rewrite the application as somehow the Titanium SDK changed enough that I couldn't get it to work. So the new code is also a lot cleaner, so maybe I could add a few features soon: 

In short this is the app.js

``` javascript app.js
Titanium.include('resource.js');
Titanium.include('parser.js');
Titanium.include('controller.js');

var controller = new Controller();
controller.start();

var webview = Titanium.UI.createWebView({url:'index.html', controller:controller});
var window = Titanium.UI.createWindow({fullscreen: true });
window.add(webview);
window.open();
```

As you see it loads the index.html which renders the main view. Index.html loads index.js which declares a listener to the update_view event.

``` javascript
Ti.App.addEventListener('update_view',function(e) {
  //..update the view using jquery based on e.state and e.info
})
```

The controller class checks every two seconds the state of the mifi card by getting the mifi status on the following url: "http://192.168.1.1/getStatus.cgi?dataType=TEXT". It then parse the data (different for each version of the card) and creates a unified javascript structure and fire the update_view event:

``` javascript
     Titanium.App.fireEvent('update_view', {state:this.currentState, info:info});     
```

To make the calls to the mifi card I wrote a Resource class that abstracts the xhr request

``` javascript
     this.mifi = new Resource("http://192.168.1.1/getStatus.cgi?dataType=TEXT");
     this.mifi.index(this.mifiResult.bind(this));
```

Internally the resource uses the createHTTPClient and makes a standard ajax get call. I haven't tried to use jquery's .get function directly but assume it may not work with Titanium without some hacking...

``` javascript
          var xhr = Titanium.Network.createHTTPClient();               
          xhr.open("GET", url);    
          xhr.send();
```

So Titanium rocks and works pretty well, at least for many iPhone apps. Now let's see how long it takes for the approval of another app that I submitted yesterday....

Enjoy!
Daniel Wanja



