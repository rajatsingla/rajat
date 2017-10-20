---
layout: post
title:  How to manage assets in rails, difference between app, vendor and lib assets, what is asset pipeline?
date:   2017-05-15 16:48:21 +0000
---


## What is assets pipeline?
In rails asset pipeline offers tools and mechanism to manage assets i.e.
JavaScript, css, image, video files. Using it you can pre-process(coffeescript,sass), compress, minify and prepare assets for use by browsers.

**Problems solved by it**

- Asset pipeline solves problem of multiple requests for each asset by compressing and compiling all alike files into one master file.
<!--more-->
- Problem of caching by adding a hash of content into the name so that browser knows when to request a new copy of file.
- Languages such as coffeescript, sass, Erb can be easily used in rails because of pre-processers provided.

---

## Asset Organization (Difference between app, vendor and lib assets)
Assets can be placed inside an application in one of three locations:
app/assets, lib/assets or vendor/assets.

- app/assets is for assets that are owned by the application, such as custom images, JavaScript files or stylesheets.
- lib/assets is for your own libraries' code that doesn't really fit into the scope of the application.
- vendor/assets is for assets that are owned by outside entities, such as code for JavaScript plugins and CSS frameworks.     

*Note: js files under app/assets will be compiled to app.js
and js files under vendor/assets to vendor.js*    

*Order in which js files are compiled is same as files are imported in application.js*
{% highlight js %}
// In application.js
//
//= require jquery
//= require jquery_ujs
//= require_tree .
//= require_tree ./components
//= require_self
{% endhighlight %}    

Make seperate folders for image,js,css files under assets folder and keep your files in respective folder. All your assets will be precompiled to public/assets from which they are served as static assets by the web server. The files in app/assets are never served directly in production.    
{% highlight ruby %}
rails-app/
    app/
        assets/
            images/      # Image assets
            javascripts/ # Custom Javascript/coffeescript
            stylesheets/ # Custom CSS/Sass
    ...
    vendor/
        assets/
            javascripts/ # Javascript libraries, etc.
            stylesheets/ # Vendor themes, javascript library theme
{% endhighlight %}    
---

Rails provide helpers to use assets in your erb files Ex.    
`.class { background-image: url(<%= asset_path 'image.png' %>) }`

---

## How to precompile assets
- In development mode, rails automatically precompiles assets on the go.     
In development mode assets are served as separate files in the order they are specified in the `application.js`.

- To use in Production you need to precompile assets by the following rake task.   
`bundle exec rake assets:precompile`

---

## css and js used for only one of the page in application, can't compile in app or vendor.js. Where to keep these files?
`Rails.application.config.assets.precompile += %w( some-other-file.js even-another.css )`    

Files you don't want to compile to a common file can be compiled seperately by adding them seperately in asset pipeline array and these files can now be used in erb files of that one particular page, like this       
`<script src="<%= asset_path 'some-other-file.js' %>"><script/>`

---

#### source
- [Asset pipeline best practices](https://launchschool.com/blog/rails-asset-pipeline-best-practices "asset pipeline best practices"){:target="_blank"}
- [Rails guide on asset pipeline](http://guides.rubyonrails.org/asset_pipeline.html "rails guide"){:target="_blank"}
