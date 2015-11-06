# コードゴルフのパーツ集

Rubyでコードゴルフを行うときに知っていると便利な知識をまとめます。

# 分岐

## 三項演算子

Bad

```ruby
if 3>2
  true
else
  false
end
```

Good

```ruby
3>2?true:false
```

## if

Bad

```ruby
n=3 if a>3
```

Good

```ruby
a>3&&n=3
```

# 文字列

## split

Bad

```ruby
"hello\nworld\nruby".split("\n") #=> ['hello', 'world', 'ruby']
```

Good

```ruby
"hello\nworld\nruby".split #=> ['hello', 'world', 'ruby']
```

Bad

```ruby
"ruby".split('') #=> ["r", "u", "b", "y"]
```

Good

```ruby
"ruby".chars #=> ["r", "u", "b", "y"]
```

# 配列

## join

Bad

```ruby
[1,2,3].join('+') #=> 1+2+3
```

Good

```ruby
[1,2,3]*'+' #=> 1+2+3
```

Very Good

```ruby
[1,2,3]*?+ #=> 1+2+3
```