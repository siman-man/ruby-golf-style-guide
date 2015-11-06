# code_golf_tips_of_ruby
Code golf tips of ruby.

# Condition

## Ternary operator

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

## Compare

Bad

```ruby
n<=0
```

Good

```ruby
n<1
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

## unless

Bad

```ruby
n=3 unless a>3
```

Good

```ruby
a>3||n=3
```

# String

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

# Array

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
