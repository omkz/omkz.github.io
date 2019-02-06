---
published: true
title: TDD dan BDD
layout: post
categories: ruby
tags: [ruby, tdd, bdd]
---


Test Driven Development (TDD) dan Behavior Driven Development (BDD) merupakan 
praktik pengembangan software dengan paradigma Agile.

**TDD adalah menulis tes terlebih dahulu, kemudian kode aplikasi** Pola TDD adalah Red/Green/Refactor, 
alurnya seperti berikut ini:

1. Menulis tes yang gagal (Red)
2. Menulis kode agar tes lulus (Green)
3. Refactor kode aplikasi untuk maintentance dan performance. Pastikan tes tetap _green_ (Refactor)

**BDD adalah teknik untuk melakukan TDD agar testing lebih mudah dipahami.** Jadi BDD merupakan pengembangan dari TDD. 
BDD mengetes perilaku(behavior) aplikasi bukan mengetes skenario tertentu.
Biasanya BDD memiliki pola Given-When-Then untuk menjelaskan sebuah tes. contoh:

```ruby
#articles.feature
Given an article exists called "Testing Demonstration"
When I visit the list of articles
Then I should see an article called "Testing Demonstration"
 
#article_steps.rb
Given /^an article exists called "(.+)"$/ do |title|
FactoryGirl.create(:article, title: title)
end
When /^I visit the list of articles$/ do
visit articles_path
end
Then /^I should see an article called "(.+)"$/ do |title|
page.should have_content title
end
```
