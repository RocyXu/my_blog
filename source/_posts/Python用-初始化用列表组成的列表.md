---
title: Python-用*复制列表
date: 2021-06-26 15:38
author: Rocy
img: /medias/featureimages/0.jpg
top: true
hide: false
cover: true
coverImg: /medias/featureimages/0.jpg
toc: true
mathjax: false
categories: python
tags:
  - python
---

## 前言
python中可以用*方便地对列表复制，但是当列表中包含列表则需注意

## 示例
在python中如果我们想对一个已有的列表复制多次，很容易想到：
```python
l = [1, 2, 3]
x = l * 5
l = [0, 0, 0]
print(l)
print(x)
# 输出
[0, 0, 0]
[1, 2, 3, 1, 2, 3, 1, 2, 3, 1, 2, 3, 1, 2, 3]
```
可见，*将l复制多次，构建一个新对象，修改l不会影响x的值，但是对于<font color="green">列表的列表</font>就需要注意：
```python
l = [[1], [2], [3]]
x = l * 5
l[0][0] = 0
print(l)
print(x)
# 输出
[[0], [2], [3]]
[[0], [2], [3], [0], [2], [3], [0], [2], [3], [0], [2], [3], [0], [2], [3]]
```
修改l的值影响到x的值，这是因为l中的元素其实是对列表的引用，x复制的也是引用

再来看看用*初始化列表，该示例来自《流畅的Python》

示例1：
```python
board = [['_'] * 3 for i in range(3)]
board[1][2] = 'X'

# 输出
[['_', '_', '_'], ['_', '_', 'X'], ['_', '_', '_']]

```

示例2：
```python
board = [['_'] * 3] * 3
board[1][2] = 'X'

# 输出
[['_', '_', 'X'], ['_', '_', 'X'], ['_', '_', 'X']]

```
示例2对列表的引用复制了3次

