---
layout: post
title: "67 Performance tips from Adobe"
date: 2011-12-15 18:51
comments: true
categories: flex
---

I just read  [Optimizing Performance for the ADOBE FLASH PLATFORM](http://help.adobe.com/en_US/as3/mobile/flashplatform_optimizing_content.pdf) from Adobe.

This is a good read and contains many useful tips and descriptions of optimization you can apply to your application. This become really relevant when developing Flex mobile applications.

Here are the 67 tips highlighted in the document... 

<!--more-->

<ol>
<li>Choose an appropriate display object.</li>
<li>Primitive types: Use the getSize() method to benchmark code and determine the most efficient object for the task.</li>
<li>Reuse objects, when possible, instead of recreating them.</li>
<li>Use object pooling, when possible.</li>
<li>Delete all references to objects to make sure that garbage collection is triggered.</li>
<li>Avoid filters, including filters processed through Pixel Bender.</li>
<li>Use mipmapping to scale large images, if needed consider creating 3D effects manually.</li>
<li>Use the Adobe® Flash® Text Engine for read-only text; use TextField objects for input text.</li>
<li>Consider using simple callbacks, instead of the event model.</li>
<li>Use the hasPriority HTML parameter to delay loading of offscreen SWF files.</li>
<li>Freeze and unfreeze objects properly by using the REMOVED_FROM_STAGE and ADDED_TO_STAGE events.</li>
<li>Use Event.ACTIVATE and Event.DEACTIVATE events to detect background inactivity and optimize your application appropriately.</li>
<li>Consider disabling mouse interactions, when possible.</li>
<li>Choose either timers or ENTER_FRAME events, depending on whether content is animated.</li>
<li>Minimize the number of Timer objects and registered enterFrame handlers in your application.</li>
<li>Stop Timer objects when not in use.</li>
<li>In enterFrame event or Timer handlers, minimize the number of changes to the appearance of display objects that cause the screen to bdrawn.</li>
<li>To save CPU power, limit the use of tweening, which saves CPU processing, memory, and battery life.</li>
<li>Use the Vector class instead of the Array class, when possible.</li>
<li>Use the drawing API for faster code execution.</li>
<li>Use event capture and bubbling to minimize event handlers.</li>
<li>Paint pixels using the setVector() method.</li>
<li>Use String class methods such as indexOf(), substr(), or substring() instead of regular expressions for basic string finding and extron.</li>
<li>Use a non-capturing group (“(?:xxxx)”) instead of a group (“(xxxx)”) in a regular expression to group elements without isolating the ents of the group in the result.</li>
<li>Consider using an alternative regular expression pattern if a regular expression performs poorly.</li>
<li>For a TextField object, use the appendText() method instead of the += operator.</li>
<li>Update text fields outside loops, when possible.</li>
<li>Avoid using the square bracket operator, when possible.</li>
<li>Inline code, when possible, to reduce the number of function calls in your code.</li>
<li>Avoid evaluating statements in loops.</li>
<li>Use reverse order for while loops.</li>
<li>Always use the redraw regions option when building your project.</li>
<li>Avoid placing content off-stage. Instead, just place objects on the display list when needed.</li>
<li>Use the appropriate Stage quality setting to improve rendering.</li>
<li>Avoid using the alpha property, when possible.</li>
<li>In general, use the lowest possible frame rate for better performance.</li>
<li>Use a low frame rate when video is the only dynamic content in your application.</li>
<li>Dynamically change the frame rate of your application.</li>
<li>Use the bitmap caching feature for complex vector content, when appropriate.</li>
<li>Set the cacheAsBitmapMatrix property when using cached bitmaps in mobile AIR apps.</li>
<li>Use the BitmapData class to create custom bitmap caching behavior.</li>
<li>Isolate events such as the Event.ENTER_FRAME event in a single handler, when possible.</li>
<li>Use the bitmap caching feature and the opaqueBackground property to improve text rendering performance.</li>
<li>Favor using asynchronous versions of operations rather than synchronous ones, where available.</li>
<li>In AIR desktop applications, consider using an opaque rectangular application window instead of a transparent window.</li>
<li>Smooth shapes to improve rendering performance.</li>
<li>Divide your application into multiple SWF files.</li>
<li>Provide event handlers and error messages for IO errors.</li>
<li>Use Flash Remoting and AMF for optimized client-server data communication.</li>
<li>Cache assets locally after loading them, instead of loading them from the network each time they’re needed.</li>
<li>Don’t change a SQLStatement object’s text property after executing it. Instead, use one SQLStatement instance for each SQL statt and use statement parameters to provide different values.</li>
<li>Use database indexes to improve execution speed for data comparing and sorting.</li>
<li>Consider pre-compiling SQL statements during application idle times.</li>
<li>Group multiple SQL data change operations in a transaction.</li>
<li>Process large SELECT query results in parts using the SQLStatement class’s execute() method (with prefetch parameter) and next() meth/li>
<li>Consider using multiple asynchronous SQLConnection objects with a single database to execute multiple statements simultaneously.</li>
<li>Avoid database schema changes.</li>
<li>Use the SQLConnection.compact() method to optimize a database after schema changes.</li>
<li>Use a fully qualified table name (including database name) in your SQL statement.</li>
<li>Use explicit column names in SQL INSERT and SELECT statements.</li>
<li>Avoid joining the same table multiple times in a statement, unless you are comparing the table to itself.</li>
<li>Use JOIN (in the FROM clause) to include a table in a query instead of a subquery in the WHERE clause. This tip applies even if you  need a table’s data for filtering, not for the result set.</li>
<li>Avoid SQL statements that can’t take advantage of indexes. These statements include the use of aggregate functions in a subquery, a UNstatement in a subquery, or an ORDER BY clause with a UNION statement.</li>
<li>Consider avoiding the LIKE operator, especially with a leading wildcard character as in LIKE('%XXXX%').</li>
<li>Consider avoiding the IN operator. If the possible values are known beforehand, the IN operation can be written using AND or OR for er execution.</li>
<li>Consider alternative forms of a SQL statement to improve performance.</li>
<li>67. Directly compare alternate SQL statements to determine which is faster.</li>
</ol>

<br/>
<p>
Enjoy!<br/>
Daniel
</p>