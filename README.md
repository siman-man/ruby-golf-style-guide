# Code Golf tips of ruby
Code golf tips of ruby.

# Remove whitespace.

There isn't need whitespace in CodeGolf.

```ruby
# bad
puts "hello world"

# good
puts"hello world"
```

# Remove parentheses

There isn't need parentheses in CodeGolf.

```ruby
# bad
puts("hello")
[1,2,3].map(&:to_s)

# good
puts"hello"
[1,2,3].map &:to_s
```

# Use shorter method name

use methods which name shorter in code golf.

```ruby
# bad
[1,2,3].find_index(2) #=> 1

# good
[1,2,3].index(2) #=> 1
```

# Command Line Option

It is important to shorten a processing of input.

bad
```ruby
while gets
  puts $_
end
```

Add option 「-n」, each input line is inserted into variable $_.

good
```ruby
#!ruby -n
puts $_
```

Add option 「-p」, At the end of program, execute 「puts $_」

very good
```ruby
#!ruby -np
```


# Variable

Variables should be defined with one character.

## define

```ruby
# bad
word='ruby'

# good
w='ruby'
```

---

if same value, variables can be declared together.

```ruby
# bad
a=3
b=3

# good
a=b=3
```

#### Multiple assignment

```ruby
a,b,c=[1,2,3]      #=> a=1, b=2, c=3
a,b,*c=[1,2,3,4,5] #=> a=1, b=2, c=[3,4,5]
a,*b,c=[1,2,3,4,5] #=> a=1, b=[2,3,4], c=5
a,*b=1             #=> a=1, b=[]
```

## Special


```ruby
# bad
a=[] #=> []

# good
$* #=> []
```

---

```ruby
# bad
ARGV

# good
$*
```

---

```ruby
# bad
"\n"

# good
$/
```

## Global

```ruby
$a=3

# bad
puts "$a is #{$a}"

# good
puts "$a is #$a"
```


# STDIO

## Output

```ruby
# bad
w="Hello Ruby!"
puts w

# good
w="Hello Ruby!"
$><<w
```

---

```ruby
# bad
10.times{puts:hello}

# good
puts [:hello]*10
```

---

```ruby
$s="Ruby"

# bad
puts $s

# good
puts$s
```

## Output(Numeric)


```ruby
# bad
puts 100

# good
p 100
```

# Condition

## Ternary operator


```ruby
# bad
if 3>2
  true
else
  false
end

# good
3>2?true:false
```

## Compare

```ruby
# bad
n<=0

# good
n<1
```

## if

```ruby
# bad
n=3 if a>3

# good
a>3&&n=3
```

## unless

```ruby
# bad
n=3 unless a>3

# good
a>3||n=3
```

# String

## split


```ruby
# bad
'hello world ruby'.split(' ') #=> ['hello', 'world', 'ruby']

# good
'hello world ruby'.split #=> ['hello', 'world', 'ruby']
```

---

```ruby
# bad
"ruby".split('') #=> ["r", "u", "b", "y"]

# good
"ruby".chars #=> ["r", "u", "b", "y"]
```

## char


```ruby
# bad
c='a'

# good
c=?a
```

## size

```ruby
# bad
"hello\n".size-1 #=> 5

# good
"hello\n"=~/$/ #=> 5
```

## symbol

```ruby
# bad
puts"ruby"

# good
puts:ruby
```

## match

```ruby
# bad
if 'ruby'=~/r/
  puts 'hello!'
end

# good
if 'ruby'[?r]
  puts 'Hello!'
end
```

---

```ruby
s="Hello Ruby"

# bad
s.gsub(/Ruby/){|m|puts m} #=> Ruby

# good
s.gsub(/Ruby/){puts $&} #=> Ruby
```

## other tips

```ruby
'hello'*0 #=> ''
'hello'*1 #=> 'hello'
'hello'*2 #=> 'hellohello'
```

# Numeric

## define

```ruby
# bad
n=10000

# good
n=1e4 #=> 10000.0
```

---

```ruby
# bad
n=0.0001

# good
n=1e-4 #=> 0.0001
```

---

```ruby
# bad
a=-10

# good
a=~9
```

---

```ruby
# bad
a=n==0?1:0

# good
a=1[n]
```

### Radix conversion

`to_s` can specify radix when convert integer to string.

```ruby
16.to_s     #=> "16"
16.to_s(2)  #=> "10000"
16.to_s(8)  #=> "20"
16.to_s(16) #=> "10"
```

## Bit operation


```ruby
n=3

# bad
(n+1)*3 #=> 12

# good
-~n*3 #=> 12
```

---

```ruby
n=3

# bad
(n-1)*3 #=> 6

# good
~-n*3 #=> 6
```

# Array

## join

```ruby
# bad
[1,2,3].join('+') #=> 1+2+3

# good
[1,2,3]*?+ #=> 1+2+3
```

## uniq

```ruby
# bad
[1,1,2,2,3,3].uniq #=> [1,2,3]

# good
[1,1,2,2,3,3]|[] #=> [1,2,3]
```

## push

```ruby
# bad
[1,2,3].push(4) #=> [1, 2, 3, 4]

# good
[1,2,3]<<4 #=> [1, 2, 3, 4]
```

## unshift

```ruby
# bad
[1,2,3].unshift(4) #=> [4, 1, 2, 3]

# good
[1,2,3][0,0]=4 #=> [4, 1, 2, 3]
```

#### compact

```ruby
p [nil,1,2,3,nil].compact #=> [1, 2, 3]
p [nil,1,2,3,nil]-[p]     #=> [1, 2, 3]
```

## define


```ruby
# bad
a=[1,2,3,4,5] #=> [1,2,3,4,5]

# good
a=[*1..5] #=> [1,2,3,4,5]
```

## reverse

```ruby
a=[1,2]

# bad
a.reverse #=> [2, 1]

# good
a.rotate #=> [2, 1]
```

---

```ruby
# bad
a=['ruby','rails','jruby']

# good
a=%w(ruby rails jruby)
```


## sum

```ruby
# bad
[1,2,3].inject(:+) #=> 6

# good
eval"[1,2,3]*?+" #=> 6

# very good (RUBY_VERSION >= 2.4)
[1,2,3].sum
```

## other

update max value

```ruby
# bad
a=[a,b+1].max

# good
a>b||a=b+1
```

# Enumerator

```ruby
n="10"
t="1"
i=0

# bad
n.to_i.times{i+=t.to_i}

# good
eval"i+=#{t};"*n.to_i
```

---

```ruby
n=5

# bad
(1..n-1).to_a #=> [1, 2, 3, 4]

# good
(1...n).to_a #=> [1, 2, 3, 4]
```


# Hash

## other

check odd? or even?

```ruby
h={}
h[1]^=1 #=> nil^1  -> true
h[1]^=1 #=> true^1 -> false
```
