+++
title = "Type Classes in Haskell"
description = "结合 Swift 中的 Protocol 来理解 Haskell 中的 type classes"
tags = [
"Haskell"
]
date = "2019-10-23"
categories = [
    "Code"
]
image = "type_classes.png"
+++

## [Haskell](https://www.haskell.org) 中的 type classes

看看 Haskell 中的求和函数:
```
sum :: (Num a) => [a] -> a
sum [] = 0
sum (x:xs) = x + sum xs
```

可以看到 sum 函数的类型签名前有对小括号 (Num a), 这个就是 Haskell 的 type classes。应该说 type classes 就是用来在泛型中限制参数类型的。因为数字可以相加，而其他类型不一定可以，比如两个人相加 (“张三” + “李四”)，结果是两个人，并不像数字 (1 + 1 = 2)一样具有合二为一的特点。

我们从 Swift 的代码更容易理解这个 type classes:
```
extension Array where Element: Numeric {
    func sum() -> Element { reduce(0, +) }
}
let intSum = [1,2,3].sum() // intSum: 6
```
一个数组是否能求和肯定是有限制的，很多数据类型不具有这样的特征，在 Swift 中使用 Protocol 来限制泛型操作中数据的类型，以上的代码意思是只有具有“数字”特征的数组才能够调用这个 sum() 函数。

结果很明显了，至少看起来 Haskell 中的 type classes 和 Swift 的 Protocol 的作用是一样的。