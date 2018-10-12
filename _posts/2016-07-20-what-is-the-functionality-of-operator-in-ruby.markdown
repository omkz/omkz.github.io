---
published: true
title: 'What is the functionality of &:  operator in ruby?'
layout: post
categories: ruby
tags: ruby

---
#that is not operator:

```ruby

ar = ["aku", "ganteng", "sekali "]

p ar.map(&:reverse) #["uka", "gnetnag", " ilakes"]
#is roughly equivalent to:
p ar.map { |element| element.reverse } #result ["uka", "gnetnag", " ilakes"]

```