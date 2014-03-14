---
layout: post
title: "Running your Flex mobile app on the iOS Emulator"
date: 2012-04-11 22:43
comments: true
categories: mobile flex
---

<p>
I just downloaded the latest AIR 3.3 and it supports running your Flex mobile apps in the iOS Emulator. If you look at Air Developer Tool help (adt -help) you get the syntax of all the commands that adt support...part of which is the following description:

<!--more-->

<div style="background:#002B36;color:#93A1A1;padding: .8em 1em;">
adt -package -target ( ipa-test | ipa-debug | ipa-app-store | ipa-ad-hoc | ipa-test-interpreter | ipa-debug-interpreter | ipa-test-interpreter-simulator | ipa-debug-interpreter-simulator ) ( CONNECT_OPTIONS? | LISTEN_OPTIONS? ) ( -sampler )? SIGNING_OPTIONS <output-package> ( <app-desc> PLATFORM-SDK-OPTION? FILE-AND-PATH-OPTIONS | <input-package> PLATFORM-SDK-OPTION? )
</div>
<p/>

<p>
For my app this translates into:

<div style="background:#002B36;color:#93A1A1;padding: .8em 1em;">
adt -package -target ipa-test-interpreter-simulator -storetype pkcs12 -keystore /Users/daniel/Desktop/certificates/daniel.p12 -storepass secret app01_ViewNavigatorApp  app01_ViewNavigatorApp-app.xml  app01_ViewNavigatorApp.swf
</div>
<p/>


This generate the app01_ViewNavigatorApp.ipa iOS app ready to be launched in the Emulator.

<p>
Then you can install the app on the emulator as follows:

<div style="background:#002B36;color:#93A1A1;padding: .8em 1em;">
adt -installApp -platform ios -platformsdk /Developer/Platforms/iPhoneSimulator.platform/Developer/SDKs/iPhoneSimulator4.3.sdk -device ios-simulator -package app01_ViewNavigatorApp.ipa
</div>
<p/>


<p>
Finally to run it:

<div style="background:#002B36;color:#93A1A1;padding: .8em 1em;">
adt -launchApp -platform ios -platformsdk /Developer/Platforms/iPhoneSimulator.platform/Developer/SDKs/iPhoneSimulator4.3.sdk -device ios-simulator -appid app01_ViewNavigatorApp
</div>
<p/>

<p>
Hope this will help you out. To find more on iOS development with Flex come see my <a href="http://www.360flex.com/schedule/">Building iPad apps with Flex</a> next week.
</p>

Enjoy!<br/>
Daniel Wanja