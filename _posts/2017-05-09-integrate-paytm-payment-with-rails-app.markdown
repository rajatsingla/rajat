---
layout: post
title:  Integrate paytm payment with rails app
date:   2017-05-09 17:44:13 +0000
---


Paytm. The fast growing payment network, it's quite easy to integrate paytm payment in your rails app.
Here is simple step by step guide on the same. 

#### 1. Register on paytm payment website.
For registering on paytm payment as a merchant you need to
[sign up here](https://paytm.com/business/payments/online), you need
1. TAN number
2. Email id
3. Website name
4. Company name.

After registration they will give you                                       

1. Category id under which your business falls
2. Merchant key
3. MID
4. Industry type
5. Staging wallet credentials
6. [Staging server URL](https://pguat.paytm.com/oltp-web/processTransaction)
7. Channel ID

#### 2. Specify the callback URL, called after payment.
You need to specify in your account, a callback url to which user will be redirected after successful payment. 
If you need to modify callback URL open a thread [here](http://paywithpaytm.com/developer/discussion/)

#### 3. Download paytm web sample kit ruby.
Download the kit [here](https://github.com/Paytm-Payments/Paytm_Web_Sample_Kit_Ruby). It gives you all the ruby code you need to integrate paytm. 

#### 4. Setup routes in routes.rb
You need to setup two routes, one for beginning payment and second for verification of payment.
<script src="https://gist.github.com/rajatsingla/e65f51e35428bc49cd809927901f142c.js"></script>

#### 5. Make a yml file with all paytm credentials.
<script src="https://gist.github.com/rajatsingla/2baac02b8ebf33dfc83af28f255feb47.js"></script>
And intialize in `application.rb`                                
`config.paytm_keys = YAML::load_file("#{Rails.root}/config/paytm.yml")[Rails.env]`

#### 6. Make a paytm controller for handling two routes.
<script src="https://gist.github.com/rajatsingla/a49010fc219919e60c380ccba959816f.js"></script>
All this code is extracted from paytm ruby kit.                                
In `start_payment` you need to make hash and from this you generate checksum hash.

#### 7. Write a helper to generate and verify checksum hash.
<script src="https://gist.github.com/rajatsingla/8f643fe297b4ac79679a474fe7466001.js"></script>
Extract `encryption_new_pg.rb` form ruby kit and add it to `app/helpers/paytm/encryption_new_pg.rb`

#### 8. Write views for two methods in paytm controller.
<script src="https://gist.github.com/rajatsingla/fb331c3558f648b089a44360b57105b0.js"></script>
<script src="https://gist.github.com/rajatsingla/625ac1d4a9897feb1200b46f2a9e71b7.js"></script>

#### 9. Add paytm payment button which initializes payment.
```
<%= form_tag paytm_payment_path, method: :post, remote: false, :style => "" do %>
			<button >Start Payment</button>
	<% end %>
```
#### 10. Summary
1. Start payment button will call start_payment method in paytm_controller
2. In start_payment method we make a hash with all values and generate checksum and then call start_payment view.
3. This view redirects to paytm payment URL with all params and checksum.
4. On staging server you need to make 3 payments with staging wallet provided by paytm.
5. After payment paytm redirects you to callback URL.
6. This calls verify_payment method which recieves all params, these all params are used to verify checksum.
7. And then we call verify_payment view.
8. Happy Coding.:)                    

Also check out paytm web integration [api page](http://paywithpaytm.com/developer/paytm_api_doc?target=transaction-request-api).
Checkout all options  you can send to payment url, like CALLBACK_URL.
Checkout payment status api which comes handy in cases of network failures. 
