---
published: true
title: How to build a Ruby hash out of two equally-sized arrays
layout: post
---
```ruby

a = [ 4, 5, 6 ]
b = [ 7, 8, 9 ]


# x = [1, 2, 3].zip(a, b) #[[1, 4, 7], [2, 5, 8], [3, 6, 9]]
# p x.class


p h = Hash[a.zip b] #{4=>7, 5=>8, 6=>9}

p h = a.zip(b).to_h #{4=>7, 5=>8, 6=>9}

p [a, b].transpose.to_h #{4=>7, 5=>8, 6=>9}

```