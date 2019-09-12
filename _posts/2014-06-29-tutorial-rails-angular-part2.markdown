---
published: true
title: Tutorial CRUD for Ruby on Rails 4 and Angular.js (part 2)
layout: post
categories: rails
tags: [rails, javascript, angular.js]
---

#### 1. buat model menggunakan generator, misal :
 
```
rails g resource book isbn:string title:string author:string publisher:string
```

lakukan migration agar table terbentuk :
```
rake db:migrate
```

#### 2. isikan sebuah data ke database. bisa diisi manual atau paka seed databasenya rails di db/seed, tambahkan beriku :
  
```
 Book.create!(isbn:'978-3-16-148410-0', title: 'rails 4 tutorial', author:'kurnia muhamad',publisher: 'majumundur')
 Book.create!(isbn:'897-5-21-982347-0', title: 'angular.js tutorial', author:'sastra djaya',publisher: 'mantapjaya')
 Book.create!(isbn:'456-7-16-093489-0', title: 'python 3 tutorial', author:'micahel heart',publisher: 'apresspub') 
 Book.create!(isbn:'977-9-45-283685-0', title: 'node.js  tutorial', author:'david HH',publisher: 'willeypub')
```

jalankan perintah :

```
rake db:seed
```
 
 
#### 3. update route menjadi berikut, karena kita mau buat aplikasi angular.js maka hanya butuh json data :

```ruby
scope :api do
  scope :v1 do
    resources :books, only: [:index], defaults: {format: :json}
  end
end
root 'home#index'
```
 
#### 4. update controller untuk menghasilkan data json :

```ruby
class BooksController < ApplicationController
   respond_to :json
 
   def index
     respond_with Book.all
   end
end

```

start server dan buka di url `http://localhost:3000/api/v1/books.json` maka data `books` akan tampil dalam bentuk `json`

#### 5. buat `books_controller.js` pada folder `assets/angular/controllers`, yang nanti `berperan` sebgai angular.js controller, isikan    sbb :

```javascript
app.controller('BooksController', ['$scope', '$resource', function($scope, $resource) {
    var Books = $resource('/api/v1/books');
    $scope.books = Books.query();
  }]);
```

#### 6. tambahkan baris berikut untuk menampilkan data di view. pada folder view home/index :
 
```erb
 <div ng-controller="BooksController">
  <ul>
    <li ng-repeat="book in books">
      {{book.title}}, {{book.author}}
    </li>
  </ul>
 </div>
```
data diatas diakses melalui ngResource module pada `books_controller.js`.
 
#### 7. sekarang kita akan menggunakan pendekatan menggunakan service angular.js. buat file `Book.js` didalam folder services dan isi :

```javascript
   app.factory('Book', ['$resource', function($resource) {
       function Book() {
           this.service = $resource('/api/v1/books/:bookId', {stockId: '@id'});
       };
       Book.prototype.all = function() {
           return this.service.query();
       };
       return new Book;
   }]);
```

dan modif `books_controller.js` menjadi :

```javascript
app.controller('BooksController', ['$scope', 'Book', function($scope, Book) {
    $scope.books = Book.all();
  }]);

```

#### 8. Sekarang kita akan membuat method DELETE.Tambahkan menu delete pada list buku :

```javascript
  <div ng-controller="BooksController">
   <ul>
    <li ng-repeat="book in books">
      {{book.title}}, {{book.author}}
      <a href="" ng-click="deleteBook(book.id, $index)">delete</a>
    </li>
   </ul>
  </div>

```

buat method untuk menghapus data pada rails di `books_controller.rb`:

```ruby
   def destroy
      respond_with Book.destroy(params[:id])
    end
  
    private
    def book_params
      params.require(:book).permit(:isbn, :title, :author, :publisher)
    end
```

jangan lupa tambahkan `strong paramater` seperti diatas kalau menggunakan rails 4.
  
- buat method delete pada `stock.js`.

```javascript
   Book.prototype.delete = function(bookId) {
        this.service.remove({bookId: bookId});
    };
```
- panggil method tersebut pada pada `books_controlle.js`:
  
```javascript
   $scope.deleteBook = function(id, idx){
        $scope.books.splice(idx, 1);
        return Book.delete(id)
    }
```
  
kemudian `start server` dan coba delete data yang ada, maka di server akan ada error :

```
  Started DELETE "/api/v1/books/6" for 127.0.0.1 at 2014-06-29 19:28:46 +0700
   Processing by BooksController#destroy as JSON
     Parameters: {"id"=>"6"}
   Can't verify CSRF token authenticity
   Completed 422 Unprocessable Entity in 1ms
   
   ActionController::InvalidAuthenticityToken (ActionController::InvalidAuthenticityToken):

```

untuk mengatasinya tambahkan method di application_controller.rb :

```ruby
  class ApplicationController < ActionController::Base
     # Prevent CSRF attacks by raising an exception.
     # For APIs, you may want to use :null_session instead.
     protect_from_forgery with: :exception
   
     after_filter :set_csrf_cookie_for_ng
     def set_csrf_cookie_for_ng
       cookies['XSRF-TOKEN'] = form_authenticity_token if protect_against_forgery?
     end
   
     protected
     def verified_request?
       super || form_authenticity_token == request.headers['X-XSRF-TOKEN']
     end
   end
```
  

