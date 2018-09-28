---
published: true
title: simple search form on rails 4
layout: post
---

home/index.html.erb

```erb
<%= form_tag(users_path, :method => "get", id: "search-form") do %>
  <%= text_field_tag :search, params[:search], placeholder: "Search Users" %>
  <%= submit_tag "Search", :name => nil %>
<% end %>
```
user.rb

```ruby
def self.search(query)
  where("name like ?", "%#{query}%") 
end
```
users_controller.rb

```ruby
def index
  if params[:search]
    @users = User.search(params[:search]).order("created_at DESC")
  else
    @users = User.all.order('created_at DESC')
  end
end
```
route.rb

```ruby
  get "/search", to: 'home#index'
```