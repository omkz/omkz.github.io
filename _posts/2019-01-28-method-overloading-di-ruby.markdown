---
published: true
title: Method overloading di Ruby
layout: post
categories: ruby
tags: [ruby, oop]
---

Banyak programmer Java yang bertanya tentang implementasi method overloading di Ruby. Method Overloading adalah Sebuah _class_ yang mempunyai 2 atau lebih method dengan nama yang sama, yang membedakan adalah argumentsnya. Yaitu jumlah dan tipe data dari arguments tersebut. Ruby tidak mendukung method overloading seperti bahasa dengan static typing. Contoh:

```ruby
def my_method(arg1)
..
end

def my_method(arg1, arg2)
..
end

my_method(10)
# Now the method call can match the first one as well as the second one, 
# so here is the problem.

```

Ruby memperlakukannya dengan cara yang berbeda.

```ruby
def my_method(*args)
  if args.length == 1
    #method 1
  else
    #method 2
  end
end
```

Cara lainnya dengan cara passing arguments sebagai sebuah hash:

```ruby
def my_method(options)
    if options[:arg1] and options[:arg2]
      #method 2
    elsif options[:arg1]
      #method 1
    end
end

#my_method arg1: 'hello', arg2: 'world'
```