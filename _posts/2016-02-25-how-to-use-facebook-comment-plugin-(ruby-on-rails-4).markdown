---
published: true
title: How to use Facebook comment plugin ( Ruby on Rails 4 )
layout: post
categories: rails
tags: [rails, facebook]

---
pertama silahkan meluncur kesini :

```
https://developers.facebook.com/docs/plugins/comments
```

klik button `Get Code` maka facebook akan menampilkan kode javascript yang harus dipasang di website kita,ex

```javascript
<div id="fb-root"></div>
<script>(function(d, s, id) {
  var js, fjs = d.getElementsByTagName(s)[0];
  if (d.getElementById(id)) return;
  js = d.createElement(s); js.id = id;
  js.src = "//connect.facebook.net/en_US/sdk.js#xfbml=1&version=v2.5&appId=474xxxxxxx";
  fjs.parentNode.insertBefore(js, fjs);
}(document, 'script', 'facebook-jssdk'));</script>
```
saya pasang kode diatas di layouts/application.html.erb sesudah tag body,
sedangkan kode dibawah ini:

```erb
<div class="fb-comments" data-colorscheme="dark" data-width="100%">
```

bisa dipasang di _comments.html.erb atau di show.html.erb sesuai dengan aplikasi anda.

perhatikan App Id sesuaikan nama aplikasi anda.

agar tidak perlu refresh ketika menampilkan facebook comment, hilangkan turbolink pada link comments

```erb
<%= link_to "comments", post, class: 'btn btn-primary', :"data-no-turbolink" => true  %>
```