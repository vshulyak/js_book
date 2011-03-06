Large scale js
===================

http://addyosmani.com/blog/large-scale-jquery/


Today we’re going to look at the end-to-end tools and options you have for building large-scale enterprise jQuery applications. Although jQuery is an excellent JavaScript library and provides a well-designed set of tools for development, it’s focus on staying compact and making the DOM easy to use has meant that it doesn’t provide a significant infrastructure for building large-scale apps.

jQuery does however normalize things across browsers and serves as a great way of doing DOM manipulation. Using it to it’s strengths, you can select some excellent tools to use along-side it as a toolkit for your larger-scale app development.


Some developers have argued in the past that building RIAs using Dojo, MooTools or YUI may be more suitable for large-scale JavaScript applications than simply opting for jQuery, however, I believe you can implement a solution using it that is equally as good without too much extra effort.

In this post we’ll be looking at ways you can put together a toolkit for large-scale jQuery application development by identifying the options you have available at the moment for dependency management, MVC with jQuery, templating, testing, minification and more.

1. Dependency Management
---------------------------

When writing large-scale jQuery applications, there may be script dependencies which you would prefer to load within a specific order or dynamically depending on their need (for a very basic example, you may wish to load functions.js before loading app.js if it relies on it) – a script loader can assist with this process. Although the traditional technique of just using hierarchially-organized script tags is equally as valid, script loaders nowadays come with a few extra features which you may find helpful, eg. loading different scripts depending on the features a browser supports or as mentioned, dynamically depending on some condition or need.

The two most dominant script loaders on the market at the moment are RequireJS (by James Burke) and LabJS (by Kyle Simpson). For quite some time there was a view that one of these had to be better than the other, but in truth, they both have their own strengths. In my experience, one of Require’s best features is it’s support of structured ‘modules’ for your code whilst LabJS is best for when you don’t need that extra feature and would prefer something more lightweight.

If you would like to read up more on whether to use Require or LabJS for your project, check out this post. For the purpose of saving you time, I’ve also included a few other options for dependancy management if these two don’t quite meet your requirements.

Options:

RequireJS – I recommend using this if you plan on keeping your code more modular. Modules attempt to limit their impact on the global namespace and be more explicit about mentioning their immediate dependencies. RequireJS also comes with an optimization tool that allows you to combine and group your scripts into a smaller set of minified scripts that load quickly - http://requirejs.org/docs/jquery.html
LabJS – this works best where scripts need to efficiently loaded in a particular order and you’re looking for a more lightweight solution than RequireJS or aren’t as interested in a modular approach to dependancy management – http://www.labjs.com (and checkout YepNope JS, an excellent conditional loader that works on top of LabJS by Alex Sexton - http://www.yepnopejs.com).
StealJS – another excellent dependancy management tool. Steal is a part of the JavaScriptMVC package but you can get it as it’s own individual package for use. Also includes concatenation, compression and code cleaning. http://jupiterjs.com/news/stealjs-script-manager
JSL Script Loader – yet another decent contenter which supports lazy lading, ordered loading, duplicate source prevention and caching. Perhaps not as extensively tested as LabJS or Require –  http://www.andresvidal.com/jsl
Bootstrap - a less feature-rich option than the others, but gets the job done. Best option if you’re looking for a very minimal solution without any of the frills https://bitbucket.org/scott_koon/bootstrap
 

2. MVC & Organization For Large-Scale jQuery Applications
---------------------------


Design patterns and Architectural patterns allow you to create re-usable, structured and more organized pieces of code based on existing tried and tested patterns in software engineering. Using a design pattern across your application is something I consider necessary especially when trying to ensure the coding style and structure is consistent when teams are involved in writing the app and not just a single person.

Quite often in modern web application development, the MVC (model-view-controller) pattern is employed for this purpose, however there exist several other popular patterns which you may find equally as useful if you feel MVC is not for you.

Below I’m going to take you through some of the MVC solutions for jQuery and JavaScript which I would recommend, however if you would like to read up some more on JS design patterns to decide on which best fits your needs, feel free to check out my free book on this topic here for more options.

MVC With JavaScript & jQuery
MVC is an architectural pattern quite often used on the server-side when creating web applications (eg. using Rails, Python, ASP.net or PHP). With this in mind, a few JavaScript developers are split as to whether jQuery-based applications need to be segmented into similar Model-View-Controller structures, or, whether they would be better suited to simply existing as more basic modular code instead.

The argument is that a clean MVC-strutured server-side codebase should suffice whilst others believe that as the complexity and scale of jQuery applications increases, especially at an enterprise level, we need a pattern like MVC in place. I agree with this latter viewpoint, although depending on the use case other patterns may be equally as useful here.

This section is directed at assisting those who have already decided they would benefit from using MVC with jQuery.

How does the MVC Pattern work?

Traditionally with MVC, you separate objects into three main categories (or concerns) when coding up your application. My interpretation of these categories is as follows:

Model – the models in your application represent knowledge and data. For example: get methods and set methods fall under this umbrella. The models are isolated and know nothing about the View nor the Controller.

View – views, from a web app perspective, can be considered the UI. They are generally dumb and don’t necessarily need to perform validation logic ie. they always forward the input via a callback system. Views are isolated and know nothing about the Model nor the Controller.

Controller – the controller sits right between the Model and the View. It performs any necessary business logic / data manipulation needed to get the data from the model to the view. The controllers do most of the validation that come back from the view and are aware of both the View and the Model.

Why I Recommend Using JavaScriptMVC For This
JavaScriptMVC has received quite a few positive reviews and is currently considered by some as the most comprehensive framework for large-scale jQuery application development available at the moment. This is a view shared by myself and a few other colleagues who have tackled larger-scale JavaScript app development in the past.

That said, if you are used to building web applications using traditional conventions (ie. heavier on the server-side, lighter on the client-side), you may find JMVC’s approach to development something which requires a small change in mindset.

For example, if a large portion of your app is JavaScript-based, keeping it modular, organized, tested and clean probably requires the use of a rolled toolkit and that’s just one of the things you get with JMVC. Most developers are probably used to catering for these things for their server-side code but the time has come for this to be considered for client-side code too.

Speaking with Justin Meyer from the JMVC project, perhaps the biggest confusion that he sees newcomers to it have is that they misunderstand exactly what the project really has to offer. In this segment of the post I would like to help clarify this.

JMVC can really be considered two things – both integrated development tools and a repeatable MVC architecture. The benefit of JMVC is that it provides a clear path to adding functionality and does a lot of the things you should be doing on your project quite easily.

First, the MVC part of JavaScriptMVC stands for the following:

Model – A way to package and organize Ajax requests and service data
Controller – A jQuery widget generator
View – Client side templates
Next, in terms of the integrated development tools that the project offers, you get the following (and more) included. While these are hardly what you would consider ground-breaking, the clean integration of such features means that you don’t have to roll your own toolkit to handle them.

Dependency management, production builds (with Less and CoffeeScript)
Automated unit and functional testing
Documentation
There are some that have commented on JMVC being ‘overkill’ as a solution. I would really only agree with this where the app you’re creating only uses a minimal amount of JavaScript or is compact enough that it may not benefit from using a managed toolkit.

For all other cases such as working with a larger-scale application, JMVC offers more than enough advantages to warrant evaluating it for your projects.

For the purpose of being extensive, I’m including a number of other options for adding MVC to your projects if you would like an alternative to JMVC.

Options:

JavaScriptMVC *(Recommended)
Mature MVC solution which includes testing, dependency management, build tools, client side templates. Perfect for large applications where an all-in-one solution for organizing and building code is required. Most recently used by Grooveshark in their app re-write.
Video Preview: http://cdn.javascriptmvc.com/videos/2_0/2_0_demo.htm
Demos and download:
 http://www.javascriptmvc.com/#&who=getcode
https://github.com/jupiterjs/srchr

Backbone 
Excellent for a DIY MVC Solution where you select the additional components you feel work best for your project. Backbone provides the ‘backbone’ you need to organize your code using the MVC pattern (but bare in mind that here the C in MVC stands for Collections and not Controllers). It’s great because it basically a provides a small framework ?(~2Kb) that provides the core pieces of KVO bindings.

Demos and download:
http://documentcloud.github.com/backbone/
http://ryandotsmith.heroku.com/2010/10/a-backbone-js-demo-app-sinatra-backend.html
http://documentcloud.github.com/backbone/docs/todos.html
http://bennolan.com/2010/11/24/backbone-jquery-demo.html

SproutCore
As it runs in the browser, SproutCore extends MVC to include a server interface, a display that ‘paints’ your interface and responders for controlling application state. Yeduha Katz who is heavily involved in the project is also working on adding modularity to SC and this option should also be available soon. Recommended for applications wishing to have a desktop-like ‘richness’. Considered overkill for smaller-sized apps. Used by Apple amongst others.
Video preview: http://vimeo.com/16774060
Demos and download:
http://wiki.sproutcore.com/w/page/12412938/Hello-World-Tutorial
http://www.sproutcore.com/get-started/

Knockout JS 
Uses MVVM (which can be considered as MVC with declarative syntax). It’s very much catered to those using JavaScript for user interfaces but does also provide dependency management, templating and works well with jQuery. May require a learning curve to get around the heavy use of data-binding.
Demos and download:
http://knockoutjs.com/documentation/introduction.htm
http://knockoutjs.com/examples/

Eyeballs JS
An MVC framework by Paul Campbell who is well known for his involvement with Ruby. Eyeballs works with many libraries but provides a layer of features for organising your code – it aims to be both agnostic and modular. About on par with Backbone. A trivial note but it’s initialization function (o_O()) may be a offputting to some. Above all, Eyeballs has quite a familiar feeling if you’re a Ruby developer and I would recommend checking it out if you primarily use Ruby for building the server-side code to your web applications.
Demos and download:
https://github.com/paulca/eyeballs.js

Sammy JS
Sammy.js is a lightweight jQuery plugin which allows you to easily define ‘route’ based applications. Where the C in MVC stands for Controller, some would consider Sammy.js the best controller framework out there but it doesn’t exactly provide the Model and View aspects itself. Sammy is still worth checking out for single page JS apps requiring a level of organization.
Demos and download:
https://github.com/quirkey/sammy

Choco
A decent looking MVC solution but needs some polish. Based on Sammy and JS-Model but comes with clean support for generators and is easily extensible.
Video Preview: http://www.2dconcept.com/images/choco.mov
Get:  https://github.com/ahe/choco



Additional pattern resources for large-scale jQuery applications:

John Resig’s Simple Inheritence
Using Inheritence Patterns To Organize Large jQuery Apps with Alex Sexton
The Object Literal pattern recommended by Rebecca Murphy
3. Templating
Templating has become a hot-topic recently in the world of JavaScript and for a very good reason – it can make it significantly easier to define a ‘template’ for data you are outputting to the browser that is substantially cleaner and more readable than simply using something such as traditional string concatanation inside an array iterating over your data object.

What are templates? Well, basically client-side templates contain mark-up with binding expressions where the template can be applied to data objects or arrays and is rendered into the HTML DOM. There are quite a few options available for using templating in your jQuery or JavaScript application, but in quite a few cases, the syntax used to define your templates doesn’t hugely differ.

The following are popular options for templating with JavaScript. I have personally found both jQuery-tmpl and Mustache the most useful in my own projects, however once again for those who feel these are overkill options, I’ve listed alternatives that you can evaluate as per your needs as well.

jQuery-tmpl http://github.com/jquery/jquery-tmpl (tutorial video here)
Mustache.js https://github.com/janl/mustache.js (tutorial video here)
Dust.js (one of Alex’s recommendations) - http://akdubya.github.com/dustjs/
Handlebars by Yehuda Katz (an extension to Mustache) - https://github.com/wycats/handlebars.js (I’m warming up to this option)
jQote http://aefxx.com/jquery-plugins/jqote/
PURE http://beebole.com/pure
Nano https://github.com/trix/nano
 

4. Communication Between Modules
---------------------------


Although this may be something you attempt to solve using a homebrewed solution, using existing pub/sub or custom events approachs are ideal for implementing simple communication between the modules in your application. Below you can find links to some different implementations of pub/sub which vary in terms of what they offer. At the moment, Ben Alman’s version is my implementation of preference as it focuses on size and utilizes jQuery custom events.

Ben Alman’s pub/sub on GitHub (this updated version contains two variations)
@phiggins jQuery.pubsub
PubSubJS
An Introduction To jQuery Custom Events
jsSignals – Custom Events/Messaging for jQuery
 

5. Build Process & Script Concatenation
---------------------------


With large-scale jQuery and JavaScript applications it’s important to have a build process in place which can assist in automating a number of tasks related to generating the final release of your code. This may not be necessary for the average website only requiring a few lines of jQuery, but serious web applications should definitely considering having a well-tuned BP in place to assist with unit testing, script concatenation, minification and other tasks. I generally recommend using ‘Ant’ for build processes as I personally believe it’s the most widely used solution of it’s kind in the JavaScript community. To get started with Ant build scripts for JavaScript projects, take a look at this helpful tutorial.

Now let’s take a look at your options for concatenation.

Ruby library for preprocessing and concatenating JavaScript source files http://getsprockets.org/
Combine and concatonate JavaScript files using Ant and YUI Compressor http://www.samaxes.com/2009/05/combine-and-minimize-javascript-and-css-files-for-faster-loading/ and http://www.javascriptr.com/2009/07/21/setting-up-a-javascript-build-process/
Using Google Closure Compiler for compile JS applictions with Ant http://groups.google.com/group/closure-compiler-discuss/browse_thread/thread/92278e7a84736f3c
Programatically concatenating files using only Ant http://stackoverflow.com/questions/1373564/how-to-programmaticly-concatenate-with-ant
Concatonate files with MVC and .NET http://www.codeplex.com/MvcScriptManager
Smasher - Smasher is a PHP5 application based on an internal tool used by Yahoo! Search. Itcombines multiple JavaScript files, preprocesses them, and optionally minifies their content. http://github.com/jlecomte/smasher
And here is another build process tool for your JavaScript applications:

Jake (used with Cappuccino): http://cappuccino.org/discuss/2010/04/28/introducing-jake-a-build-tool-for-javascript/
 

6. Script Minification
---------------------------


Minification is a critical part of the build process for any large jQuery application. When delivering scripts in a live production environment (especially one which you may get a lot of traffic to), every extra byte counts, which is why you should ideally minify your code rather than just including the unminified/uncompressed version that requires your users to spend longer waiting for it to download.

The minification process can sometimes require a little tool tweaking to get the most out of it, but trust me when I say that this time can be well worth the investment. It might be interesting to note that over at jQuery, we are constantly testing new minification tools and a tool is never something set in stone – just because you opt for Google’s Closure compiler in 2010 doesn’t mean you might not shift to UglifyJS in 2011 for example. Your build process can be flexible enough to accomodate these changes.

Remember that minification is ideally done as part of a script concatenation step so factor this in too (Note: JavaScript MVC covers both these steps if you are opting to use MVC in your application).

Options:

Google Closure Compiler http://code.google.com/closure/compiler/
YUI Compressor http://developer.yahoo.com/yui/compressor/ (and automating this with Packer here)
Minifier http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=34488
UglifyJS * (Recommended as it shows promising minification gains on the others) https://github.com/mishoo/cl-uglify-js
Packer for .NET http://svn.offwhite.net/trac/SmallSharpTools.Packer/wiki
Dojo Toolkit’s ShrinkSafe http://www.dojotoolkit.org/
JSMin – The JavaScript minifier http://www.crockford.com/javascript/jsmin.html
 

7. Testing
---------------------------


Production-ready jQuery applications need to be heavily tested to ensure that your code both works *and* performs as expected – this is especially critical when writing large-scale apps as you don’t want your users first experience to be of your application falling over.

Before we get deeper into this section, I should say that regardless of how complete your test coverage is, nothing really beats having a human that didn’t write your code go through and test your code/application out. That said, let’s take a look at further testing options.

Unit testing is something I suggest as a must but in this section I’m also going to include links to resources on other aspects of testing jQuery apps which may come in helpful depending on what you’re doing.

Unit Tests For Your JavaScript/jQuery Code Using QUnit

A solid build process with unit-testing should be used for testing and releasing any serious jQuery application. Manual functional testing is great from a user-interface perspective, but Unit testing will allow you to stress-test your code to find out if all the inner-workings of it perform as intended. Below is a good tutorial on how to get started with QUnit – a popular jQuery Unit testing tool which is quite straight-forward to use. You may alternatively like to check out JSUnit or FireUnit but QUnit is by far the most widely used of the three and my personal unit testing tool of choice.

http://net.tutsplus.com/tutorials/javascript-ajax/how-to-test-your-javascript-code-with-qunit/

Unit Testing With FuncUnit From JavaScriptMVC

FuncUnit, as recommended by Alex, allows you to easily manipulate elements and fake aspects such as user interaction quite well.FuncUnit itself is an add-on to QUnit and the tests you create with it can be run in the browser or with Selenium. It also allows you to automate basic QUnit tests in EnvJS (a commend line browser).  We recommend checking it out

http://jupiterjs.com/news/funcunit-fun-web-application-testing

Mock Your Ajax Requests with MockJax & jQuery for Rapid Development

The MockJax plugin is a really fantastic development and testing tool for intercepting and simulating ajax requests made with jQuery with a minimal impact on changes to production code. I recommend this for testing web applications that frequently use Ajax connections. TamperData is also useful for testing of this type. Read the complete tutorial on using MockJax below.

http://enterprisejquery.com/2010/07/mock-your-ajax-requests-with-mockjax-for-rapid-development/

Getting Started With Test-Driven Development For jQuery

The concept of test-driven development is quite simple. Anytime you want to add a new feature to your application, you need to write a test for it before writing any code for that feature. To write the test, you need to fully understand the specifications and requirements for what that feature does. At the start, your test will of course fail, but the goal is to ultimately code up a solution to that feature which is considered finished if the test passes. Here is an excellent tutorial on how to get started with test-driven development for jQuery with Elijah Manor.

http://msdn.microsoft.com/en-us/scriptjunkie/ff452703.aspx

Automating jQuery testing with Browser Launching, Test Execution And Result Reporting

If building a large-scale web application that heavily relies on JavaScript, chances are you’ll want to test your code in a number of different web browsers but also on a number of different platforms. You can achieve this without needing to do a lot of manual work using a number of existing frameworks. John Resig recommendsWebDriver (Java), Watir (Ruby) and JSTestDriver for achieving these. Selenium RC is also popular for this purpose. These are the best tools to use if testing is performed in-house. If you’re looking to use an external source of systems for your testing, see the next section.

Debugging And Testing JavaScript In A Scripting Environment With Envjs and BumbleBee

Envjs is a tool which provides a JavaScript implementation of the browser as a usable scripting environment. This enables developers to effectively run jQuery and JavaScript in a console which can be useful for debugging purposes. The default implementation of Envjs is Rhino.

Rhino (Java) is a great tool for running JavaScript in either shell form or embedded in other applications – in shell form it can be used as the debugger mentioned above. Rhino basically converts JavaScript code into Java classes and its primarily intended to be used in server-side applications. If your build process is based on using ANT or something similar, placing Rhino’s JAR file into your classpath would allow your build to execute JavaScript.

A good testing toolkit for Envjs is BumbleBee which was released this year. Bumblebee combines Rhino, JSpec, Envjs and Ant to provide an "out of the box" JavaScript testing toolkit where specs can easily be added to your automated build. I recommend checking it out!.

jQuery Driven Automated User Interface Testing

UITest is a recommended automated UI testing framework for jQuery projects written by Menno van Slooten. While quite young in terms of it’s maturity, you can find some good examples of how to use this framework on the official github page or via Menno’s original talk on the topic from his jQuery Bay Area Conference slides here. You can also find out some additional recent information on user-interface testing for generic JavaScript applications at this post which discusses Selenium and Coded UI as alternatives.

https://github.com/mennovanslooten/UITest

 

Conclusions
---------------------------


I hope you’ve found this guide to building large-scale jQuery applications useful. Whilst a single all-encompassing solution may very be something desirable to the community at large, the aim of this post was to provide you with all of the options that are (to my knowledge) available for both rolling your own large-scale toolkit for application development.

Providing you and your team with the flexibility to decide is the most useful thing that could be done with this information and in that regard, I hope I’ve managed to trim down some of the time you may have otherwise spent researching this topic.

At the end of the day, if you are looking for an all-inclusive solution, JavaScriptMVC is probably the closest thing available to a mature, well-supported option and I encourage you to check it out if you feel it would benefit you more than a custom-rolled toolkit would. Remember that while comprehensive, JMVC is also completely modular. What this means is that if you desired, you could just take FuncUnit, the Controller and StealJS and use them as your own personal toolkit without much heavy-lifting at all. 

Whatever direction you do take with building your large-scale application, know that there are enough tools and resources within the JavaScript community to help get you started.

 

Further Reading & Resources
On jQuery and large applications with Rebecca Murphy
On ‘Rolling Your Own’ Large jQuery Apps with Alex Sexton
jQuery UI Developer’s Guide (for those wishing to use $.widget etc)
Nicholas Zakas – Scalable JavaScript Application Architecture
Tech Behind The New GrooveShark (Good Article On Large Scale jQuery App Dev)
Cody Lindley’s excellent list of client-side development links for app development
JavaScript Documentation Tools: JSDoc, YUI Doc or PDoc
 

And that’s it!. I would like to extend my thanks to Alex Sexton, Dan Heberden and Justin Meyer for their assistance with parts of this post. If you found it helpful, please feel free to hit the reweet button to share it with your friends and colleagues. Until next time, good luck with your JavaScript & jQuery apps!.
