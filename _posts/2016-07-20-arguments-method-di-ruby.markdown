---
published: true
title: arguments method di ruby
layout: post
---
## 1. single asterisk atau splat operator (*args)

jika kita memberikan argument pada method yang mempunyai splat operator, maka argument tersebut akan otomatis di ubah menjadi sebuah array. perhatikan contoh berikut:

```ruby
def my_method(*args)
  p args
  p args.class
end

my_method(1, "3", nama: 'paijo')
# [1, "3", {:nama=>"paijo"}]
# Array
```

disini argument apapun akan diterima dan otomatis akan dijadikan sebuah array.

## 2. double asterisk atau double operator (**args)

method ini meminta sebuah hash sebagai argument, perhatikan contoh berikut:

```ruby
def my_method(**args)
  p args
  p args.class
end

my_method(1, "3", nama: 'paijo')
#in `my_method': wrong number of arguments (2 for 0) (ArgumentError)
```

error akan muncul jika kita memasukan argument selain hash.
contoh yang benar:
```ruby
def my_method(**args)
  p args
  p args.class
end

my_method(nama: 'paijo')
# {:nama=>"paijo"}
# Hash
```
tidak semua argument di terima sebagai inputan. hanya `hash` saja

## 3. : parameter

akan meminta argument dengan key yang sesuai dengan di parameter. jika tidak dipenuhi akan memicu error `missing keyword:  (ArgumentError)`

```ruby
def my_method(name:)
  p name
end

my_method
# in `<top (required)>': missing keyword: name (ArgumentError)
```

## 4. ampersand parameter (&)
menjadikan block sebagai sebuah parameter, contoh:

```ruby
def my_method(&block)
  yield if block_given?
end

my_method do
  puts "hello"
end

#hello
```
hasil yang sama juga akan diperoleh dengan:

```ruby
def my_method(&block)
  block.call
end
```

atau:
```ruby
def my_method
  yield
end
```






