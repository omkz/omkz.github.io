---
published: true
title: render partial :object vs :locals on Rails
layout: post
---

```erb
<%= render :partial => 'partial/path', :locals => {:xyz => 'abc'} %>
```
vs

```erb
<%= render :partial => 'partial/path', :object => @some_object %>
```

`:locals => {:xyz => 'abc'}` makes the variable xyz available in the partial(and the value is 'abc').

using `:object` will define a variable with the same name as the partial by default. 

```erb
render :partial => 'account', :object => @some_account
```

will make sure the account variable in the partial will be set to @some_account. You can rename the variable using the :as option.

The biggest advantage of the `:locals`is that

 1. you have very clear control over the objects and names
 2. you can assign more than 1 variable
 So you could do something like

render partial => 'some_view', :locals => { :user => account.user, :details => some_details_we_retrieved }
making a clear seperation possible when needed.

The disadvantage of the :locals approach is that it is more verbose, and sometimes a simple

```erb
render :partial => 'account'
```
is identical to

```erb
render :partial => 'account', :locals => {:account => @account }
```
So use the one which suits you the best (or where it suits the best).