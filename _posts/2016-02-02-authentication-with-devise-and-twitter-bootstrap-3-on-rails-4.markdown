---
published: true
title: Authentication with Devise and Twitter Bootstrap 3
layout: post
categories: rails
tags: [rails, devise, twitter bootstrap 3]
---

here is application.html.erb

```erb
<!DOCTYPE html>
<html>
<head>
  <title>Social</title>
  <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track' => true %>
  <%= javascript_include_tag 'application', 'data-turbolinks-track' => true %>
  <%= csrf_meta_tags %>
</head>
<body>
<%= render 'shared/navbar' %>
<%= render 'shared/messages' %>

<div class="container">
  <%= yield %>
</div>
</body>
</html>
```

_shared/navbar.html.erb

```erb
<nav class="navbar navbar-default navbar-fixed-top">
  <div class="container">
    <div class="navbar-header">
      <%= link_to 'Social', root_path, class: 'navbar-brand' %>
    </div>
    <div id="navbar">
      <ul class="nav navbar-nav">
        <li><%= link_to 'Home', root_path %></li>
        <li><%= link_to 'Trending', "#" %></li>
      </ul>
      <ul class="nav navbar-nav pull-right">
        <% if user_signed_in? %>
            <li class="dropdown">
              <a class="dropdown-toggle" data-toggle="dropdown" href="#">
                <%= current_user.email %>
                <span class="caret"></span>
              </a>
              <ul class="dropdown-menu" role="menu">
                <li><%= link_to 'Profile', edit_user_registration_path %></li>
                <li><%= link_to 'Log out', destroy_user_session_path, method: :delete %></li>
              </ul>
            </li>
        <% else %>
            <li><%= link_to 'Log In', new_user_session_path %></li>
            <li><%= link_to 'Sign Up', new_user_registration_path %></li>
        <% end %>
      </ul>
    </div>
  </div>
</nav>
```

_shared/messages.html.erb

```erb
<div class="container">
  <% flash.each do |key, value| %>
      <div class="alert alert-<%= key %>">
        <%= value %>
        <button type="button" class="close" data-dismiss="alert" aria-hidden="true">&times;</button>
      </div>
  <% end %>
</div>
```


style.css

```scss
body {
  padding-top: 100px;
  font-family: 'Noto Sans', sans-serif;
}

.alert-alert {
  @extend .alert-warning;
}

.alert-notice {
  @extend .alert-info;
}
```
