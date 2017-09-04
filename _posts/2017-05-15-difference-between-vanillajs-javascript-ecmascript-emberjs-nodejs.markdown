---
layout: post
title:  Difference between vanilla.js, javascript, ecmascript, ember.js, node.js
date:   2017-05-15 16:47:47 +0000
---


## Vanilla.js
[Vanilla.js](http://vanilla-js.com/){:target="_blank"} is nothing but a name given to the **practice of using plain JavaScript**
without any additional JavaScript libraries as a mockery to remind
framework lovers that many things can be done without the need for additional JavaScript
libraries.  
<!--more-->

---
## ECMAScript
[ECMAScript](https://en.wikipedia.org/wiki/ECMAScript){:target="_blank"} is a **standard followed by JavaScript language**.
ECMAScript is standardized by Ecma International in ECMA-262, So that every browser follows this standard.
There is no compiler out there that would run ECMAScript,
and I believe JavaScript is considered the Language which implements a standard called ECMAScript.   
**Latest released edition of es is ES6**, adds significant new syntax for writing complex applications.  
Example:
{% highlight js %}
var name = "Bob", time = "today";
`Hello ${name}, how are you ${time}?`
{% endhighlight %}
- [all es6 features](https://github.com/lukehoban/es6features "es6 features"){:target="_blank"}   
For browsers that do not suppport es6 you can use babel to transpile code to es5.

---
## JavaScript
**[JavaScript](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/JavaScript_basics){:target="_blank"} is a high-level, dynamic, untyped, and interpreted programming language**.
It has been standardized in the ECMAScript language specification.
Alongside HTML and CSS, JavaScript is one of the three core technologies of World Wide Web content production;
the majority of websites employ it, and all modern Web browsers support it without the need for plug-ins.

---
## ember.js
[Ember](http://emberjs.com/){:target="_blank"} or react.js or angular.js are **open-source JavaScript web frameworks** to make ambitious app.
Based on the Modelâ€“viewâ€“viewmodel (MVVM) pattern. It(Ember) allows developers to create
scalable single-page web applications by incorporating common idioms and best practices into the framework.

---
## node.js
[node.js](https://en.wikipedia.org/wiki/Node.js){:target="_blank"} is a **JavaScript runtime** built on chrome's
[v8 engine](https://en.wikipedia.org/wiki/V8_(JavaScript_engine)){:target="_blank"}.
It is used to run JavaScript on server side and for developing various type of tools and applications.
Node.js has an event-driven architecture capable of asynchronous I/O.
These design choices aim to optimize throughput and scalability in Web applications with many input/output operations,
as well as for real-time Web applications (e.g., real-time communication programs and browser games).
express.js is a web framework for node.js     
