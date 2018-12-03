---
title: 那些踩过的python坑
date: 2018-12-03 15:14:53
tags: python
categories:
- language
- python
---

## 列表

### 列表复制和删除

```Python
a = [1,2,3,4,5]
b = a
b.remove(3)
a
a = [1,2,4,5]
# 解决办法是调用copy函数，然后再进行删除的时候就不会这样了
b = a.copy()
```

### List Set Dict Tuple的区别和用法

- List: 不要求元素类型一样，是有序的,使用[]

  - 常用方法：append(value)，insert(pos,value)，pop(index)

- Tuple: 可以看成一种不变（不可变指的是指向的位置不可变）的"List",是用()，也是通过下标访问，元素是固定的

  ```Python
  t = (3.14, 'China', 'Jack', ['a','b'])
  L = t[3]
  L[0] = 122
  print(t)
  (3.14, 'China', 'Jack', [122, 'b'])
  ```

- Dict：活字典，可以添加键值对，是无序的，key不可变，value可变，查找速度快

- set：内容元素不重复

  - 常用方法：add(value)，[已经有不会报错，但不会加进去],remove(value),[没有会报错]
  - 交集：a.intersection(b); 并集： a.union(b); 差集： a.differecnce(b)

