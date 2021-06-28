---
title: Python-字典键值不存在时的处理
date: 2021-06-27 15:38
author: Rocy
img: /medias/featureimages/1.jpg
top: true
hide: false
cover: true
coverImg: /medias/featureimages/1.jpg
toc: true
mathjax: false
categories: python
tags:
  - python
---

## 前言
python中经常会出现字典键值不存在的情况，可以用`get(), setdefault(), defaultdict`等方式处理

## 示例
示例1：
```python
my_dict = {
    'a': [1],
}

b = my_dict.get('b', [])
b.append(0)

print(b)
print(my_dict)
# 输出
[0]
{'a': [1]}

```
my_dict不存在键`'b'`, 使用`dict.get()`处理键不存在情况会返回一个默认值，但是不会向`my_dict`添加新的键值对

示例2：
```python
my_dict = {
    'a': [1],
}

b = my_dict.setdefault('b', [])
b.append(0)
my_dict.setdefault('b', []).append(3)

print(b)
print(my_dict)
# 输出
[0, 3]
{'a': [1], 'b': [0, 3]}
```
使用`dict.setdefault()`则会添加新的键值对

对于需要处理键不存在的情况，使用`collections.defaultdict`处理更加自然一些, 参考：
https://docs.python.org/2/library/collections.html
示例3：
```python
import collections

my_dict = collections.defaultdict(list)
x = my_dict['a']
print(x)
# 输出
[]
```
键值不存在时，表达式`my_dict['a']`按照一下步骤执行：
- 调用`list()`创建一个新对象
- 把新对象作为值，向my_dict添加新的键值对
- 返回该对象的引用

也可以使用自定义类，例如示例4：
```python
import collections

class A():
    def __init__(self):
        self.a = 1
        self.b = 2


my_dict = collections.defaultdict(A)
x = my_dict['a']
print(x.a)
# 输出
1
```

