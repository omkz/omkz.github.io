---
published: true
title: Creating Like Button Using Acts_as_votable Gem On Ruby On Rails
layout: post
---

likes_controller.rb

```ruby
def upvote
    @post = Post.find(params[:id])
    @post.upvote_by current_user

    respond_to do |format|
      format.js{}
    end
  end
```

home/index.html.erb

```ruby
<% @posts.each do |post| %>
    <div class="row">
      <div class="col-lg-7 well">
        <h3>
          <%= post.title %>
        </h3>
        <p>
          <%= image_tag(post.image_url) if post.image? %>
        </p>
        <div class="like" id="<%= post.id %>">
          <%= render partial: 'likes/form', locals: {:@post => post}%>
        </div>
        
    </div>
    </div>
<% end %>
```

partial page likes/form.html.erb

```ruby
<% if current_user.liked? @post %>
    <%= link_to unlike_like_path(@post), method: :put, class: 'btn btn-info liked', remote: true do %>
        <%= fa_icon 'thumbs-up' %> liked
    <% end %>
<% else %>
    <%= link_to like_like_path(@post), method: :put, remote: true, class: 'btn btn-info' do %>
        <%= fa_icon 'thumbs-up' %> like
    <% end %>
<% end %>
```

like.js.erb

```javascript
$('.like#<%= @post.id %>').html('<%= j render "form", locals: { post: @post } %>');

```

routes.rb

```ruby
resources :likes do
    member do
      put "like", to: "likes#like"
      put "unlike", to: "likes#unlike"
    end
  end
```