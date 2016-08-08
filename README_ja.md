# Code Golf tips of ruby
Rubyのコードゴルフでの役立つ情報をまとめます

# コマンドラインオプション

入力を受け取って値を出力するタイプの問題の場合は入力の処理を短くすることも大事です

bad
```ruby
while gets
  puts $_
end
```

オプション -n を指定することで、入力の各行の内容が$_に入ってプログラムが実行されます。

good
```ruby
#!ruby -n
puts $_
```

オプション -p をつけることでプログラムの最後の処理に「puts $_」が実行されるようになります

very good
```ruby
#!ruby -np
```

# 変数

## 定義

変数名は基本1文字で定義しましょう。

```ruby
# bad (変数名が長すぎる)
name='siman'

# good
n='siman'
```

---

同じ値を宣言する場合はまとめたほうがいいです

```ruby
# bad
a=3
b=3

# good
a=b=3
```

## 特殊変数

Ruby自身に最初から組み込まれている変数には、ゴルフで利用できる便利なものがそろっています。

### 配列
```ruby
# bad (長い)
a=[]

# good
$*
```

---

プログラムで渡された引数を受け取ります

```ruby
# bad (長い)
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

## グローバル変数

```ruby
$a=3

# bad
puts "$a is #{$a}"

# good - グローバル変数は{}を省略しても参照できます
puts "$a is #$a"
```

# 標準入出力

## 出力

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

# good - 配列に対してputsを行うと、各要素からto_sを呼び出したものを出力します
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

## 出力(数値)

```ruby
# bad
puts 100

# good - 数値を出力する場合はpメソッドが短くて良いです
p 100
```

# 条件式

## 三項演算子

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

## 比較演算子


```ruby
# bad
n<=0

# good
n<1
```

## if

短絡評価を使用することで分岐が実現できます

```ruby
# bad
n=3 if a>3

# good - 左側が偽の場合は右側を評価しなくても偽になるので評価されない
a>3&&n=3
```

## unless

```ruby
# bad
n=3 unless a>3

# good - 左側が真の場合は右側を評価してなくても真になる
a>3||n=3
```

# 文字列(String)

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
"ruby".split('') #=> ['r', 'u', 'b', 'y']

# good
"ruby".chars #=> ['r', 'u', 'b', 'y']
```

## 文字(Char)

```ruby
# bad
c='a'

# good - 「?」+「文字」で1文字を定義することができる
c=?a
```

## size

```ruby
# bad
"hello\n".size-1 #=> 5

# good
"hello\n"=~/$/ #=> 5
```

## シンボル(symbol)


```ruby
# bad
puts"ruby"

# good - putsするとシンボルでも同じ結果になります
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

## その他

```ruby
# 文字列に対して数値をかけるとその文字列が繰り返されます
'hello'*0 #=> ''
'hello'*1 #=> 'hello'
'hello'*2 #=> 'hellohello'
```

# 数値(Numeric)

## 宣言

```ruby
# bad
n=10000

# good - 1 * (10 ** 4)を表します
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

# good - 数値に対して[]メソッドを適用すると、指定した位置のビットの値が参照できます
a=1[n]
```

## ビット演算

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

# 配列(Array)

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

# good - 2つの要素に限ってrotateが短い
a.rotate #=> [2, 1]
```

---

```ruby
# bad
a=['ruby','rails','jruby']

# good - %wな記法に置き換えることで短くなります
a=%w(ruby rails jruby)
```

## unshift

```ruby
# bad
a=[1,2,3]
a.unshift(4) #=> [4,1,2,3]

# good
a=[1,2,3]
a=[4]+a #=> [4,1,2,3]
```

## sum

```ruby
# bad
[1,2,3].inject(:+) #=> 6

# good - evalを使って式の評価を行います
eval"[1,2,3]*?+" #=> 6
```

## index

Rubyでは同じ動作でもっと短い関数名が存在していたりします。

```ruby
# bad
[1,2,3].find_index(2) #=> 1

# good
[1,2,3].index(2) #=> 1
```

## その他

最大値の更新

```ruby
# bad
a=[a,b+1].max

# good
a>b||a=b+1
```

# 繰り返し(Enumerator)

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

# good - 終端を含みたくない場合は...を使う
(1...n).to_a #=> [1, 2, 3, 4]
```


# ハッシュ(Hash)

## other

check odd? or even?

```ruby
h={}
h[1]^=1 #=> nil^1  -> true
h[1]^=1 #=> true^1 -> false
```
