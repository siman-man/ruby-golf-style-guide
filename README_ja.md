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

# split

Bad

```ruby
"hello\nworld\nruby".split("\n") #=> ['hello', 'world', 'ruby']
```

Good

```ruby
"hello\nworld\nruby".split #=> ['hello', 'world', 'ruby']
```
