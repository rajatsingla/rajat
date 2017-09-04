---
layout: post
title:  Sessions and csrf in rails.
date:   2017-05-15 16:45:40 +0000
---


Most apps need to be able to store some data about a user. Maybe itâ€™s a user id, or a preferred language.
session is the perfect place to put this kind of data.
Little bits of data you want to keep around for more than one request.

`Sessions` are easy to use:
<!--more-->
{% highlight ruby %}
session[:current_user_id] = @user.id
{% endhighlight %}

## What is a session?


<b>A session is just a place to store data during one request that you can read during later requests.</b>

You can set some data in a controller action:

>app/controllers/sessions_controller.rb
{% highlight ruby %}
def create
  # ...
  session[:current_user_id] = @user.id
  # ...
end
{% endhighlight %}

And read it in another:
>app/controllers/users_controller.rb
{% highlight ruby %}
def index
  current_user = User.find_by_id(session[:current_user_id])
  # ...
end
{% endhighlight %}

It might not seem that interesting.
But it takes coordination between your userâ€™s browser and
your Rails app to make everything connect up.
And it all starts with `cookies`.

## Cookie?
When you request a webpage, the server can set a cookie when it responds back.   
Your browser will store those cookies.
And until the cookie expires,
every time you make a request,
your browser will send the cookies back to the server.
<b>This cookie contains your rails session you have been using.</b>

*****

## Cross-Site Request Forgery
Lets say you are logged in on gmail.com and in
another tab you have opened a hackerâ€™s website. Which is urging you to
click a image saying you will get 100 coins. But actually it will send a
request to gmail.com deleting all mails. This request will be successful
 because browser will send cookie along with the request
 and in this cookie your current gmail session exists.

## How to prevent CSRF?
 Synchronizer token pattern (STP) is a technique where a token, secret and unique value for each request, is embedded by the web application in all HTML forms and verified on the server side.

## How does the token look like?
The token will be added automatically to every form like this:     
`<input name="authenticity_token" type="hidden" value="OXuQV+9Q1hi5YkeynLQgVddCRfdUwl0huvqSjoqf4mE=" />.`    
The same token is in user's session. On every request the token in session and the token in HTML form are compared on the server side and if they match
only then the request is completed.**The purpose of the token is that an attacker doesnâ€™t know the victimâ€™s
token and thus a CSRF attack without that token would be refused.**

## Protect CSRF in Rails app
The CSRF protection can be turned on with the `protect_from_forgery` controller method  and is included in the `ApplicationController` by default.
So for every non-GET (and non-HEAD) action Rails will check the authenticity token.
{% highlight ruby %}
class ApplicationController < ActionController::Base
  # Prevent CSRF attacks by raising an exception.
  # For APIs, you may want to use :null_session instead.
  protect_from_forgery with: :exception
end
{% endhighlight %}





source:   
<a href="http://www.rorsecurity.info/">http://www.rorsecurity.info/</a>
<br>
<a href="http://www.justinweiss.com/articles/how-rails-sessions-work/">http://www.justinweiss.com/articles/how-rails-sessions-work/</a>
<br>
<a href="http://guides.rubyonrails.org/security.html">http://guides.rubyonrails.org/security.html</a>
