# コードゴルフのパーツ集

Rubyでコードゴルフを行うときに知っていると便利な知識をまとめます。

# 分岐

## 三項演算子

Bad

```Ruby
if 3>2
  true
else
  false
end
```

Good

```Ruby
3>2?true:false
```

## if

Bad

```Ruby
n=3 if a>3
```

Good

```Ruby
a>3&&n=3
```
