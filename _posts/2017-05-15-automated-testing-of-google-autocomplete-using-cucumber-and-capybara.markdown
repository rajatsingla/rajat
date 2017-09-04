---
layout: post
title:  Automated testing of google autocomplete using cucumber and capybara
date:   2017-05-15 16:48:47 +0000
---


Ruby script for automated testing of google autocomplete in HTML form using cucumber and capybara.      
Add the following script for google autocomplete.
<!--more-->

***
>google_autocomplete.feature

{% highlight ruby %}
Scenario: S1
    And I fill google autocomplete
{% endhighlight %}

>google_autocomplete.rb

{% highlight ruby %}
module name
  def fill_google_autocomplete(id)
    sleep 1
    ele=find(id)
    if ele
      ele.set "delhi"
      sleep 1
      ele.native.send_keys(:arrow_down)
      ele.native.send_keys(:return)
    end
    sleep 1
  end
end

World(name)

Then /^I fill google autocomplete$/ do
    fill_google_autocomplete("#location-div")
end
{% endhighlight %}
