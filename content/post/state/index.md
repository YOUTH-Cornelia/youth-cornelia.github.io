---
title: "State control"
date: 2026-03-03
draft: false
categories: ["9021"]
tags: ["9021"]
---

## 关于普通编程题中的“状态”:

可以是 true/false 也可以是一个 
### 第一题
```python
# 旋转字符串
def rotations(n):
    # 循环
    # 切片
    n_str = str(abs(n))
    res = []

    for _ in range(len(n_str)):

        if n > 0:
            res.append(int(n_str))
        else:
            res.append(int(n_str) * -1)

        if n > 0:
            n_str = n_str[-1] + n_str[:-1]
        else:
            n_str = n_str[1:] + n_str[0]
            
    return res

```


### lab2第二题（COMP9021）
### Quiz2第一题（COMP9021）
### Leetcode（896.单调数列）

[Leetcode 896: Monotonic array](https://leetcode.cn/problems/monotonic-array/description/?envType=study-plan-v2&envId=programming-skills)
（也有单独的讲解）
```python
class Solution:
    def isMonotonic(self, nums: List[int]) -> bool:
        gap = nums[-1] - nums[0]
        if gap < 0:
            tr = -1
        else:
            tr = 1
        for i in range(1,len(nums)):
            if (nums[i]-nums[i-1])*tr < 0:
                return False
        return True
```
```python
class Solution:
    def isMonotonic(self, nums: List[int]) -> bool:
        increasing = True
        decreasing = True        
        for i in range(0, len(nums) - 1):
            if nums[i] > nums[i + 1]:
                increasing = False
            if nums[i] < nums[i + 1]:
                decreasing = False
        return increasing or decreasing
```

### 参考模版

1. 判断出现多次

2. 规则复杂

3. 后续行为依赖这个判断

4. 你发现代码开始重复

```python
初始化状态
循环
    根据状态决定行为
    更新状态
返回结果
```
```
state = ...

for ...:
    if state:
        ...
    else:
        ...

    state = 更新(state)
```
or
```
while ...:
    ...
```
> 当你发现以下的时候就代表可能可以优化成这个状态的形式了，就算是if n > 0这种的其实也是一个状态判断，这个时候运用状态就是去优化，但有时候状态就是逻辑的一部分，方便解题，而不是解题方法。

> 这个变量，是不是为了“记住过程中的信息”？如果是 → 必须状态，如果不是 → 可能只是优化






