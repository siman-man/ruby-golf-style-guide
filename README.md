# Code Golf tips of ruby
Code golf tips of ruby.

# STDIO

## Output

Bad

```ruby
w="Hello Ruby!"
puts w
```

Good

```ruby
w="Hello Ruby!"
$><<w
```

Bad

```ruby
10.times{puts:hello}
```

Good

```ruby
puts [:hello]*10
```

## Output(Numeric)

Bad

```ruby
puts 100
```

Good

```ruby
p 100
```

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
'hello world ruby'.split(' ') #=> ['hello', 'world', 'ruby']
```

Good

```ruby
'hello world ruby'.split #=> ['hello', 'world', 'ruby']
```

Bad

```ruby
"ruby".split('') #=> ["r", "u", "b", "y"]
```

Good

```ruby
"ruby".chars #=> ["r", "u", "b", "y"]
```

## char

Bad

```ruby
c='a'
```

Good

```ruby
c=?a
```

## symbol

Bad

```ruby
puts"ruby"
```

Good

```ruby
puts:ruby
```

# Numeric

Bad

```ruby
n=10000
```

Good

```ruby
n=1e4 #=> 10000.0
```

Bad

```ruby
n=0.0001
```

Good

```ruby
n=1e-4 #=> 0.0001
```

## Bit operation

Bad

```ruby
n=3
p (n+1)*3 #=> 12
```

Good

```ruby
n=3
p -~n*3 #=> 12
```

Bad

```ruby
n=3
p (n-1)*3 #=> 6
```

Good

```ruby
n=3
p ~-n*3 #=> 6
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

## define

Bad

```ruby
a=[1,2,3,4,5] #=> [1,2,3,4,5]
```

Good

```ruby
a=1,2,3,4,5 #=> [1,2,3,4,5]
```

Very Good

```ruby
a=[*1..5] #=> [1,2,3,4,5]
```

## sum

Bad

```ruby
[1,2,3].inject(:+) #=> 6
```

Good

```ruby
eval"[1,2,3]*?+" #=> 6
```

## index

Bad

```ruby
[1,2,3].find_index(2) #=> 1
```

Good

```ruby
[1,2,3].index(2) #=> 1
```
