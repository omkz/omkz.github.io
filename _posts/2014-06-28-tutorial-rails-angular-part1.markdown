---
published: true
title: tutorial crud rails and angular.js Part 1
layout: post
---
#### 1. pertama buka terminal

#### 2. ketikan command. karena saya anti TDD :D maka beri parameter -T

```
rails new RailsAngularCrudTutorial -T 
```

#### 3. pasang gem angularjs-rails di gemfile :

```
gem 'angularjs-rails'
```

run bundle install

#### 4. buat folder `angular` didalam `app/assets/javascripts`. Didalam folder `angular` buat folder `controllers, services` jika diperlukan. buat juga main.js di dalam foder javascript

- tambahkan pada `application.js` menjadi :

```
//= require angular
//= require angular-resource
//= require main.js
//= require_tree ./angular
//= require_tree .
    
```

#### 5. generate controller menggunakan command :

```
rails g controller home index
```

edit konfigurasi routes.rb agar controller tersebut menjadi default :

```
root 'home#index'
```
    
#### 6. tampahkan skrip berikut di main.js dengan skrip berikut :

```
var app = angular.module("RailsAngular", ['ngResource']);
```

#### 7. di view, folder layouts/application ganti baris <html> dengan :
    
```
<html ng-app="RailsAngular">
```

`ng-app="RailsAngular"` harus sama dengan nama module di `main.js`
    
#### 8. di bagian view, folder home/index ganti menjadi :
    
```
<h1>welcome,</h1>
<form>
<input type="text" ng-model='name' placeholder="Enter a name">
<input type="submit" value="Add">
</form>
{{ name }}
```

sekarang coba jalankan aplikasi dan inputkan nama anda di textinput .. voila . .. .selanjutnya di part 2 kita akan bertemu database 