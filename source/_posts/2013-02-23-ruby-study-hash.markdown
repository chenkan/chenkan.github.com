---
layout: post
title: "Ruby学习系列 - 基础知识 - Hash"
date: 2013-02-23 21:56
comments: true
categories: 51-Ruby
---

### 序言

这部分讲`Hash`，取材于[Ruby core API](http://www.ruby-doc.org/core-1.9.3/Hash.html)，加以归纳整理，便于记忆

### 赋值

``` ruby
h = { "a" => 100, "b" => 200 }
h["a"] = 9
h["c"] = 4
h   #=> {"a"=>9, "b"=>200, "c"=>4}
```

### 取值

```
h = { "a" => 100, "b" => 200 }
h["a"]   #=> 100
h["c"]   #=> nil
```
```
h = { "a" => 100, "b" => 200, "c" => 300, "d" => 300 }
h.key(200)   #=> "b"
h.key(300)   #=> "c"
h.key(999)   #=> nil
```

### 运算

```
h1 = { "a" => 100, "b" => 200 }
h2 = { "b" => 254, "c" => 300 }
h1.merge(h2)   #=> {"a"=>100, "b"=>254, "c"=>300}
h1.merge(h2){|key, old_val, new_val| new_val - old_val}
               #=> {"a"=>100, "b"=>54,  "c"=>300}
h1             #=> {"a"=>100, "b"=>200}
```

### 增减

```
h = { "a" => 100, "b" => 200 }
h.delete("a")                              #=> 100
h.delete("z")                              #=> nil
```
```
h = { "a" => 100, "b" => 200, "c" => 300 }
h.delete_if {|key, value| key >= "b" }   #=> {"a"=>100}
```

`reject!` is equivalent to `Hash#delete_if`, but returns `nil` if no changes were made.

### 统计与查询

```
{}.empty?   #=> true
```

```
h = { "a" => 100, "b" => 200 }
h.has_key?("a")   #=> true
h.has_key?("z")   #=> false
```
```
h = { "a" => 100, "b" => 200 }
h.has_value?(100)   #=> true
h.has_value?(999)   #=> false
```

```
h = { "a" => 100, "b" => 200, "c" => 300, "d" => 400 }
h.keys   #=> ["a", "b", "c", "d"]
```
```
h = { "a" => 100, "b" => 200, "c" => 300 }
h.values   #=> [100, 200, 300]
```

```
h = { "d" => 100, "a" => 200, "v" => 300, "e" => 400 }
h.length        #=> 4
h.delete("a")   #=> 200
h.length        #=> 3
```

```
h = { "a" => 100, "b" => 200, "c" => 300 }
h.select {|k,v| k > "a"}  #=> {"b" => 200, "c" => 300}
h.select {|k,v| v < 200}  #=> {"a" => 100}
```

### 其它

```
h = { "a" => 100, "b" => 200 }
h.each {|key, value| puts "#{key} is #{value}" }
```
```
h = { "a" => 100, "b" => 200 }
h.each_key {|key| puts key }
```
```
h = { "a" => 100, "b" => 200 }
h.each_value {|value| puts value }
```

### 小结

以上为不完全统计，后续调整