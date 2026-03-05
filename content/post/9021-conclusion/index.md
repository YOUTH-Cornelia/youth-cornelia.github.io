---
title: "9021基础思路总结"
date: 2026-03-05
draft: false
categories: ["9021"]
tags: ["9021"]
---


## 基础编程思维结构（非算法类）（基础）

### 1、收集结果（最基础）

**模板**

```python
res = []

for x in data:
    if condition:
        res.append(x)
```
**列表生成式：**
```python
res = [x for x in data if condition]
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

### 2、累计计算（计数 / 求和）(和defaultdic集合)

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

# 3、状态变量（State Variable） / 状态模拟

很多题的核心是 **记录当前状态，并根据输入不断更新状态**。

状态变量可以是：

```text
布尔值（True / False）
计数值（count）
符号 / 方向（sign / direction）
```

这些变量用来 **记录之前发生了什么，从而影响后续逻辑**。

### 基本模板

```python
state = initial_state

for x in data:
    if condition:
        state = new_state
```

也可以根据状态执行不同逻辑：

```python
state = initial_state

for x in data:
    if state:
        do_something()

    if condition:
        state = new_state
```

### 常见状态类型

### 1、布尔状态（True / False）

表示某种条件是否成立。

例子：句子首字母大写

```python
capitalise_next = True

for word in words:
    if capitalise_next:
        word = word.capitalize()

    capitalise_next = word[-1] in ".?!"
```

这里的状态是：

```
是否需要大写
```

### 2、计数状态（count）

用于记录某种数量。

例子：括号匹配

```
遇到 '('
count += 1

遇到 ')'
count -= 1
```

当：

```
count == 0
```

说明一段括号结束。


### 3、符号 / 方向状态

用于记录趋势或方向。

例如单调数组判断，正负数分类：（等）

```
sign = 1   # increasing
sign = -1  # decreasing
```

或者：

```
direction = right
direction = left
```

其实，状态变量本质上是：**记录历史信息**，

例如：

```
括号已经打开多少个
是否处于句子开始
当前序列是递增还是递减
```

这些信息 **无法只靠当前元素判断**，必须用状态变量记录。


### 总结：

状态模拟的核心是：

```
扫描数据
根据当前元素更新状态
根据状态决定行为
```

```
很多“触发事件（trigger）”的题其实也是状态变化
例如：
句子结束
括号匹配
分组结束
```

### 4、枚举 + 验证（很多题的核心）

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


### 5、分组（字典用法 + append）

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

### 6、二维列表结构

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

### 7、双指针 / 相邻元素比较（Pointer Scan）

常用于：
相邻元素比较、
区间扫描、
数组趋势判断、
字符串扫描

注意避免：`index out of range`

* 相邻元素比较（`i` 和 `i+1`）
* 两个指针移动（`left / right`）

### ① 相邻元素比较（最常见）

**模板**

```python
for i in range(len(L)-1):
    if L[i] > L[i+1]:
        ...
```

例子（判断单调数组）

```python
for i in range(len(nums)-1):
    if nums[i] > nums[i+1]:
        print("not sorted")
```

例如：
monotonic array、
连续字符、
趋势判断

### ② 双指针扫描（two pointers）

用两个指针控制区间：

```
left
right
```

**模板**

```python
left = 0
right = len(L) - 1

while left < right:
    ...
```

常见用途：
回文判断、
区间收缩、
两端扫描

例如回文：

```python
left = 0
right = len(s) - 1

while left < right:
    if s[left] != s[right]:
        return False
    left += 1
    right -= 1
```

### 这一类题的本质

其实都是：**用索引控制扫描**

可以是：
`
i
i,i+1
left,right`

本质就是：`index scan`

### 总结

这一类题通常是：

```
通过索引访问相邻或两端元素
进行比较或移动
```


### 8、构造字符串（这个可能没有什么的）

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

字符串是不可变对象，大量拼接时效率较低，
复杂情况可以使用 list + join。
```python
res = []

for x in data:
    res.append(x)

result = ''.join(res)
```

### 9、索引访问（最常见）

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


### 10、zip / zip_longest（并行处理）
>打印题, 字符对齐, 多列数据处理

**zip：** `zip` 会在最短序列结束时停止，同时遍历两个序列。

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

其中`itertools.zip_longest`就是它的扩展版本，代表着遍历最长序列短的序列用填充值补齐。

基本用法：
```python
from itertools import zip_longest

for a, b in zip_longest(A, B, fillvalue=''):
    ...
```
通常在打印输出题里用的多（模拟按照列打印）
（eg.
每一行变成列表
zip_longest 对齐
fillvalue='' 补空）
如果需要视觉对齐，通常需要先使用
ljust / rjust / center
把字符串补齐长度（`x.ljust(length, “需要被填充的东西，可以是空格”)`）,否则 zip_longest 只是补空，不会自动对齐。
例子：

```python
length = 8
number = 7
binary = f"{number:0b}"
print("1" * (length - len(binary)) + binary) #1111111
print(binary.ljust(length,"1"))  #1111111
```

### 11、切片模式
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

### 12、移动控制（Movement）+ 边界检查（Boundary Check）
> 很好的例子，楼梯图像的匹配，二维数组的路径（这个也有可能是递归）
还有就是spiral matrix
当然，这个边界检查也包含那种list的out of index。
前面写过怎么判断这个控制这个边界。
字符串扫描、窗口扫描、矩阵路径题、spiral / grid / maze`(if not valid: change direction)`

### 核心思维：
```
当前位置 (r, c)
↓
尝试往当前方向走
↓
检查是否有效 (valid)
    valid → 继续走
    invalid → 改变方向
```

常见写法：
```
当前位置 (r,c)

计算下一步 (nr,nc)

if valid(nr,nc):
    移动
else:
    改变方向
```

### valid 判断通常包含:
> (看到 grid 题会马上想到去先写valid的条件)

1. 没有越界
2. 没有访问过
3. 满足题目条件

```python
0 ≤ r < rows
0 ≤ c < cols
```

### 方向在代码中的表示（direction vector）:
不是必须用“指针”， 用`方向 = 向量(dr, dc)`

### 一、最常见方式：方向向量（推荐理解）

方向通常用 **两个变量表示移动量**：

```text
dr = row change
dc = column change
```

例如：

| 方向 | dr | dc |
| -- | -- | -- |
| 右  | 0  | 1  |
| 下  | 1  | 0  |
| 左  | 0  | -1 |
| 上  | -1 | 0  |

这样移动就是：

```text
r = r + dr
c = c + dc
```

所以：

```text
下一步 = 当前坐标 + 方向向量
```

这是最常见的表示方式。

### 二、方向数组（spiral常用）

因为方向是循环的，所以通常写成一个列表：

```text
directions = [
    (0,1),   # right
    (1,0),   # down
    (0,-1),  # left
    (-1,0)   # up
]
```

然后用 **一个变量表示当前方向**：

```text
d = 0
```

表示：

```
当前方向 = directions[d]
```

换方向就是：

```
d = (d + 1) % 4
```

这就是 spiral 最常见写法。

### 三、简单情况：直接用 if 判断

有些题没有方向循环，只是两种选择。

例如楼梯搜索：

```text
如果 value > target
    往左
否则
    往下
```

这种情况其实没有“方向状态”，
只是 **条件决定移动**。

### 四、所以方向其实就是一种“状态变量”

就像之前说的：

```
state
```

例如：

```
direction = right
```

或者：

```
d = 0
```

然后每一步：

```
根据 direction 计算下一步
```


### 五、统一理解移动类题

所有移动题其实都是：

```
当前位置 (r,c)
+
方向 (dr,dc)
```

得到：

```
下一位置
```

如果不能走：

```
改变方向
```

### 六、spiral 的真正思维结构

其实就是：

```
当前位置
+
方向向量
=
下一位置
```

如果下一位置不合法：

```
方向换成下一方向
```

### 七、为什么这样设计

因为这种表示方式：

```
非常统一
非常简洁
```

你只需要改变：

```
dr, dc
```

就能改变方向。

### 八、很多算法题都是这样表示方向

例如：

### spiral matrix

```
右 → 下 → 左 → 上
```

### BFS grid

```
上 下 左 右
```

### knight move

```
8个方向
```

其实全部都是：

```
方向向量
```

### 九、总结一句话

方向在代码里通常表示为：

```python
(dr, dc)
```

表示：

```
行变化
列变化
```

移动就是：

```python
(r + dr, c + dc)
```

---

### 大多数 Python 编程题，本质是以下结构的组合：

```
扫描 (for)
状态 (state)
收集 (append)
统计 (count)
分组 (dict)
索引访问 (index)
边界控制 (boundary)
```

看到题目先判断：

```
① 要不要收集结果 → append
② 要不要统计数量 → count
③ 要不要分组 → dict + append
④ 要不要模拟过程 → 状态变量
⑤ 要不要试所有情况 → 枚举
```
