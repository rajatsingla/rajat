---
layout: post
title:  Best practices while using ooor gem for making rpc calls to odoo(openerp) from ruby framework
date:   2017-05-15 16:44:22 +0000
---


# Best practices while Using Ooor gem for making rpc calls to Odoo(openerp) from ruby framework


Odoo(openerp) is a management software written in python using xml and qweb engine.
Odoo is all the rage for ERP back-offices, but sometimes you want freedom and scalablity for your web front ends which you can achieve by Odoo data access JSON API.

Odoo provides all of its data from the outside for external analysis or integration with various tools. Model Reference API is easily available over XML-RPC and accessible from a variety of languages.

Odoo requires users of the API to be authenticated before they can query most data.         
In ruby you can use `XMLRPC::Client` to query data.

### Making a connection
```ruby
require "xmlrpc/client"
common = XMLRPC::Client.new2("#{url}/xmlrpc/2/common")
uid = common.call('authenticate', db, username, password, {})
```
### Making a call
```ruby
models = XMLRPC::Client.new2("#{url}/xmlrpc/2/object").proxy
models.execute_kw(db, uid, password,
    'res.partner', 'check_access_rights',
    ['read'], {raise_exception: false})
```
More on [Api integration]       
But using this you have to handle all the parllel processing and complexity inherent with XML-RPC

This is where Ooor comes in, It doesn't embed any business rule, it's just a client to Odoo. The code of Ooor is modeled after Rails ActiveModel, ActiveResource and ActiveRecord layers.
It loads Odoo models into proxy Activeresource objects in rails.
ProductProduct for the product.product Odoo model.
Ooor emulates the ActiveRecord API wherever possible delegating its requests to Odoo using Odoo domain S expressions instead of SQL.

### Add gem to gemfile
`gem 'ooor'`


### Standalone Ruby application
```ruby
require 'rubygems'
require 'ooor'
Ooor.new(:url => 'http://localhost:8069/xmlrpc', :database => 'mybase', :username => 'admin', :password => 'admin')
```
This will load all models of Odoo with admin access right because we have made a connection by admin's account.        
Now you should be able to access `ResUsers.find(1)`

**Note:** Ruby proxy objects are named after Odoo models in but removing the '.' and using CamelCase. (we remind you that OpenERP tables are also named after OpenERP models but replacing the '.' by '_'.) `eg. res.users to ResUsers`

### Usage
You can use all common orm methods(create,find,browse,read) available in Odoo on loaded proxy objects. Ooor provide support for context,relations,domain.                         
Like            

```ruby
ResPartner.search([['name', 'ilike', 'a']], 0, 2)
ResPartner.find(:all, :params => {:supplier => true})
ProductProduct.find(1).categ_id # where categ_id is inherited from the ProductTemplate
pc = ProductCategory.new(:name => 'Categ From Rails!')
#<ProductCategory:0xb702c42c @prefix_options={}, @attributes={"name"=>"Categ From Rails!"}>
pc.create
pc.id
```
More on [Common orm methods]

Ooor provides all support for domain search on proxy objects.
```ruby
ProductProduct.find(:all, :domain=>[['categ_id','=',1],'|',['name', '=', 'PC1'],['name','=','PC2']])
```
More on [Domains] 

You can also execute ActiveRecord methods on proxy objects but it is generally advised to stick with common orm methods of Odoo.

### Extending the OOOR models
Odoo model get a basic ActiveResource model. For instance: product.product is mapped to the ProductProduct ActiveResource model. Using the Ruby open classes features, you can re-open the ProductProduct class and add features of your own.
```ruby
class ProductProduct < OpenObjectResource
   def foo
     "bar"
   end
end
```
Now a ProductProduct resource got a method foo, returning "bar".
### Using Ooor results in views 

Using results of Ooor proxy object is exactly as you would use any other activeresource object's results                           
Like
```ruby
class ProductProductController 
   def index
     @products=ProductProduct.all
   end
end

#in views
<% for i in @products %>
<%= i.name%>
<% end %>
```

More on [Ooor]

[Domains]:  <https://www.odoo.com/documentation/8.0/reference/orm.html#domains>
[common orm methods]: <https://www.odoo.com/documentation/8.0/reference/orm.html#common-orm-methods>
[ooor]: <https://github.com/akretion/ooor>
[api integration]: <https://www.odoo.com/documentation/8.0/api_integration.html>