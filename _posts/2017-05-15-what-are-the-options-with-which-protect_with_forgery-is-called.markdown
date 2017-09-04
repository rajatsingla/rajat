---
layout: post
title:  What are the options with which protect_with_forgery is called?
date:   2017-05-15 16:46:43 +0000
---


{% highlight ruby %}
class ApplicationController < ActionController::Base
  # Prevent CSRF attacks by raising an exception.
  # For APIs, you may want to use :null_session instead.
  protect_from_forgery with: :exception
end
{% endhighlight %}

**What happens if the token is missing or wrong** depends on the option with
 which protect_from_forgery method is called.     
 In Rails there are three options: Throw an exception, create a new session or clear the current session.
<!--more-->
 - `protect_from_forgery with: :null_session` (dafault option)
 Set all values to nil in all cookies, including the session.
 That means the user wonâ€™t be logged in anymore for that action and
canâ€™t perform the change (if the action requires a signed in user).

- `protect_from_forgery with: :reset_session`
Rails set a new cookie with empty session in browser.That means the user wonâ€™t be logged in anymore.     
`small hack` If user copies old cookie before forgery attack, he can reset user session after attack.

- `protect_from_forgery with: :exception` Raises an ActionController::InvalidAuthenticityToken exception.

For a user related rails application `with: :null_session` is adviced

We may want to disable CSRF protection for APIs since they are typically designed to be state-less.
 That is, the request API client will handle the session for you instead of Rails.

Else the nature of your app decides which option is best.  
