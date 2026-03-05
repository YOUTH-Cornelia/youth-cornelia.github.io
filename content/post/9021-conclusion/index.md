---
title: "9021基础思路总结"
date: 2026-03-05
draft: false
categories: ["9021"]
tags: ["9021"]
---


## **Python做题最核心的 10 个结构模板**。
### **思维模式分类**

# 1、收集结果（最基础）

**模板**

```python
res = []

for x in data:
    if condition:
        res.append(x)
```

**作用**

```
过滤 / 收集
```

**例子**

```python
nums = [1,2,3,4]

res = []
for n in nums:
    if n % 2 == 0:
        res.append(n)
```

结果

```
[2,4]
```
# 2、累计计算（计数 / 求和）

**模板**

```python
count = 0

for x in data:
    if condition:
        count += 1
```

**作用**

```
统计数量
```

例子

```python
count = 0
for n in nums:
    if n % 2 == 0:
        count += 1
```

# 3、状态变量（COMP9021最常见）

**模板**

```python
state = something

for x in data:
    if condition:
        state = new_state
```

例子（句子首字母大写）

```python
capitalise_next = True

for word in words:
    if capitalise_next:
        ...
    capitalise_next = word[-1] in ".?!"
```

这就是你之前写的：

```
状态模拟
```

# 4、枚举 + 验证（很多题的核心）

**模板**

```python
for candidate in possibilities:
    if valid(candidate):
        ...
```

例子

```
找因数
找组合
找排列
```

例如

```python
for i in range(1, n+1):
    if n % i == 0:
        print(i)
```

你之前说的 **枚举 + 验证**就是这个。


# 5、分组（字典 + append）

**模板**

```python
groups = {}

for x in data:
    key = rule(x)
    groups.setdefault(key, []).append(x)
```

例子

```python
words = ['apple','banana','avocado']

groups = {}

for w in words:
    groups.setdefault(w[0], []).append(w)
```

结果

```
{
'a':['apple','avocado'],
'b':['banana']
}
```

# 6、二维列表结构

**模板**

```python
matrix = [[] for _ in range(n)]

for x in data:
    matrix[i].append(x)
```

例子

```python
matrix = [[] for _ in range(3)]

for i in range(6):
    matrix[i%3].append(i)
```

结果

```
[[0,3],
 [1,4],
 [2,5]]
```

# 7、双指针 / 相邻比较

**模板**

```python
for i in range(len(L)-1):
    if L[i] > L[i+1]:
        ...
```

例子

```python
for i in range(len(nums)-1):
    if nums[i] > nums[i+1]:
        print("not sorted")
```

你之前的：

```
monotonic array
```

就是这个。

# 8、构造字符串

**模板**

```python
res = ""

for x in data:
    res += something
```

例子

```python
binary = ""

while n > 0:
    binary = str(n % 2) + binary
    n //= 2
```

# 9、索引访问（最常见）

**模板**

```python
for i in range(len(L)):
    ...
```

例子

```python
for i in range(len(words)):
    if words[i][-1] == '.':
        ...
```

---

# 10、zip / zip_longest（并行处理）

**模板**

```python
for a, b in zip(A, B):
    ...
```

例子

```python
A = [1,2,3]
B = [4,5,6]

for x,y in zip(A,B):
    print(x+y)
```

其中

```
zip_longest
```

就是它的扩展版本。


# 11、切片模式
- 左旋
`s[1:] + s[0]`
- 右旋
`s[-1] + s[:-1]`
- 删除一个元素
`L[:i] + L[i+1:]`
- 子串扫描
`s[i:i+k]`
- 反转
`s[::-1]`


Python题 **90%是这些结构组合**：

```
for循环
状态变量
append
字典分组
索引访问
```

例如一个典型题：

```python
groups = {}

for word in words:
    key = len(word)
    groups.setdefault(key, []).append(word)
```

其实就是：

```
for循环
分组
append
```

三种结构叠加
---

看到题目先判断：

```
① 要不要收集结果 → append
② 要不要统计数量 → count
③ 要不要分组 → dict + append
④ 要不要模拟过程 → 状态变量
⑤ 要不要试所有情况 → 枚举
```
