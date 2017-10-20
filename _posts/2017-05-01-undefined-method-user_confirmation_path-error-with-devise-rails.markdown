---
layout: post
title:  Undefined method `user_confirmation_path' error with devise rails.
date:   2017-05-01 09:45:06 +0000
---


#### Common errors in devise
1. undefined method `user_confirmation_path`
2. undefined method `current_user`
3. undefined method `authenticate_user`

#### Common reasons for these errors
1. Make sure your devise model's name is user and not something like service_user.
2. Make sure you have defined routes `devise_scope :service_user do` in routes.rb. You can check the same by running rake routes.
3. Make sure you have generated views `rails generate devise:views users`
4. Make sure you have configured model [configuring models](https://github.com/plataformatec/devise#configuring-models) 
5. Make sure you have restarted the server after these changes.