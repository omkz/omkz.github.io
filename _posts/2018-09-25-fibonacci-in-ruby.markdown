---
published: true
title: Fibonacci Sequence in Ruby
layout: post
categories: ruby
tags: [ruby, algorithm]
---

 Fibonacci atau sering disebut deret atau bilangan fibonacci adalah sebuah deret bilangan yang memiliki pola tertentu, yaitu sebuah suku ke -n , merupakan hasil penjumlahan dari suku (n-1) dengan suku (n-2). berikut adalah contohnya:

```
1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610, 987 ...
```

dalam contoh diatas bisa dilihat bahwa angka 8(suku ke 6) diperoleh dari 5 (suku ke-5) + 3(suku ke-4). jadi rumusnya adalah:

```
f(n) = f(n-1)+f(n-2)
```

maka contoh implementasinya di ruby adalah sebagai berikut:

```ruby

def fib(n)
  if n <=2
    n =1
  else
     fib(n - 1) + fib(n - 2)
  end
end

p (1..150).map {|i| fib(i)} 

```

yang menjadi masalah dengan kode diatas adalah perfomanya yang lambat karena fungsi yang rekursif. berikut adalah contoh optimasi fungsi tersebut menggunakan teknik memoization agar loadnya lebih cepat:

```ruby

def fib(n, cache = {})
  return 1 if n <= 2
  cache[n] ||= fib(n-1, cache) + fib(n-2, cache)
end

p (1..1000).map {|i| fib(i)}

```

Referensi:
- https://devblast.com/b/ruby-fizzbuzz-fibonacci