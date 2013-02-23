---
layout: post
title: "Ruby学习系列 - 基础知识 - Array"
date: 2013-02-20 22:37
comments: true
categories: 51-Ruby
---

### 序言

本着赶鸭子上架及边学边做的精神，总也算是写了好一些Ruby代码；但回过头来发现自己的进步不大，写代码还是很生涩，不上道，多次在基础知识上摔跟头

新的一年开始了，希望自己能够扎实掌握Ruby这项技能，从基础开始，梳理一些知识点

第一部分讲`Array`，取材于[Ruby core API](http://www.ruby-doc.org/core-1.9.3/Array.html)，加以归纳整理，便于记忆

### 创建

If multiple copies are what you want, you should use the block version which uses the result of that block each time an element of the array needs to be initialized:

``` ruby
a = Array.new(2) { Hash.new }
a[0]['cat'] = 'feline'
a # => [{"cat"=>"feline"}, {}]
```

### 赋值

```
a = Array.new
a[4] = "4";                 #=> [nil, nil, nil, nil, "4"]
a[0, 3] = [ 'a', 'b', 'c' ] #=> ["a", "b", "c", nil, "4"]
a[1..2] = [ 1, 2 ]          #=> ["a", 1, 2, nil, "4"]
a[0, 2] = "?"               #=> ["?", 2, nil, "4"]
a[0..2] = "A"               #=> ["A", "4"]
a[-1]   = "Z"               #=> ["A", "Z"]
a[1..-1] = nil              #=> ["A", nil]
a[1..-1] = []               #=> ["A"]
```

### 取值

```
a = [ "a", "b", "c", "d", "e" ]
a[1, 2]                #=> [ "b", "c" ]
a[1..3]                #=> [ "b", "c", "d" ]
a[-3, 3]               #=> [ "c", "d", "e" ]
```

```
a = [ "q", "r", "s", "t" ]
a.first     #=> "q"
a.first(2)  #=> ["q", "r"]
```

```
a = [ "w", "x", "y", "z" ]
a.last     #=> "z"
a.last(2)  #=> ["y", "z"]
```

### 运算

```
[ 1, 2, 3 ] + [ 4, 5 ]    #=> [ 1, 2, 3, 4, 5 ]
[ 1, 1, 2, 2, 3, 3, 4, 5 ] - [ 1, 2, 4 ]  #=>  [ 3, 3, 5 ]
[ 1, 2, 3 ] * 3    #=> [ 1, 2, 3, 1, 2, 3, 1, 2, 3 ]
[ 1, 1, 3, 5 ] & [ 1, 2, 3 ]   #=> [ 1, 3 ]
```

### 增减

```
[ 1, 2 ] << "c" << "d" << [ 3, 4 ] #=>  [ 1, 2, "c", "d", [ 3, 4 ] ]
```

```
a = [ "a", "b", "b", "b", "c" ]
a.delete("b")                   #=> "b"
```

```
a = %w( ant bat cat dog )
a.delete_at(2)    #=> "cat"
a                 #=> ["ant", "bat", "dog"]
```

```
a = [ "a", "b", "c" ]
a.delete_if {|x| x >= "b" }   #=> ["a"]
```

```
reject {|item| block } → new_ary
reject → an_enumerator
```
Returns a new array containing the items in self for which the block is not true. See also `Array#delete_if`

If no block is given, an enumerator is returned instead.

```
reject! {|item| block } → ary or nil click to toggle source
reject! → an_enumerator
```
Equivalent to `Array#delete_if`, deleting elements from self for which the block evaluates to true, but returns nil if no changes were made. The array is changed instantly every time the block is called and not after the iteration is over. See also Enumerable#reject and Array#delete_if.

```
a = %w{ a b c d }
a.insert(2, 99)         #=> ["a", "b", 99, "c", "d"]
a.insert(-2, 1, 2, 3)   #=> ["a", "b", 99, "c", 1, 2, 3, "d"]
```

```
a = [ "a", "b", "c" ]
a.slice!(1)     #=> "b"
a               #=> ["a", "c"]
a.slice!(-1)    #=> "c"
a               #=> ["a"]
a.slice!(100)   #=> nil
a               #=> ["a"]
```

```
a = [ "a", "b", "c", "d" ]
a.pop     #=> "d"
a.pop(2)  #=> ["b", "c"]
a         #=> ["a"]
```

```
a = [ "a", "b", "c" ]
a.push("d", "e", "f") #=> ["a", "b", "c", "d", "e", "f"]
```

```
args = [ "-m", "-q", "filename" ]
args.shift     #=> "-m"
args           #=> ["-q", "filename"]
```
```
args = [ "-m", "-q", "filename" ]
args.shift(2)  #=> ["-m", "-q"]
args           #=> ["filename"]
```

### 变换

```
a = [ "a", "b", "c", "d" ]
a.collect {|x| x + "!" }   #=> ["a!", "b!", "c!", "d!"]
a                          #=> ["a", "b", "c", "d"]
```

```
a = [ "a", "b", "c", "d" ]
a.collect! {|x| x + "!" }
a             #=>  [ "a!", "b!", "c!", "d!" ]
```

`collect`等效于`map`

```
[ "a", "b" ].concat( ["c", "d"] ) #=> [ "a", "b", "c", "d" ]
```

```
[ "a", "b", "c" ].join        #=> "abc"
[ "a", "b", "c" ].join("-")   #=> "a-b-c"
```

```
[ "a", "b", "c" ].reverse   #=> ["c", "b", "a"]
```

```
a = [ "a", "b", "c" ]
a.reverse!       #=> ["c", "b", "a"]
a                #=> ["c", "b", "a"]
```

```
a = [ "d", "a", "e", "c", "b" ]
a.sort                    #=> ["a", "b", "c", "d", "e"]
a.sort {|x,y| y <=> x }   #=> ["e", "d", "c", "b", "a"]
```

```
a = [ "a", "a", "b", "b", "c" ]
a.uniq   # => ["a", "b", "c"]
```

```
b = [["student","sam"], ["student","george"], ["teacher","matz"]]
b.uniq { |s| s.first } # => [["student", "sam"], ["teacher", "matz"]]
```

### 统计与查询

```
ary = [1, 2, 4, 2]
ary.count             #=> 4
ary.count(2)          #=> 2
ary.count{|x|x%2==0}  #=> 3
```

```
a = [ "a", "b", "c" ]
a.include?("b")   #=> true
a.include?("z")   #=> false
```

```
[ 1, 2, 3, 4, 5 ].length   #=> 5
```

```
a = %w{ a b c d e f }
a.select {|v| v =~ /[aeiou]/}   #=> ["a", "e"]
```

```
[].empty?   #=> true
```

### 其它

```
a = [ "a", "b", "c" ]
a.each {|x| puts x }
```

```
a = [ "a", "b", "c" ]
a.each_index {|x| puts x } # passes the index of the element instead of the element itself
```

### 小结

`Array`包含很多API，以上只是我个人当前认为比较常用的一部分，后续会再调整

下面介绍`Hash`与`String`
