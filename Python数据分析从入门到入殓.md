# Python数据分析从入门到入殓



​	数据分析就是让数据数据产生价值，通过数据的筛选、汇总等等操作从而分析或预测出事件的变化规律。Python语言在数据分析领域同样扮演者比较强大的角色，其中被熟知的主要有三个扩展库用来做数据分析，分别是：`Pandas`、`Numpy`、`Matplotlib`，其中，`Pandas`主要是用作提炼数据使用、`Numpy`则提供强大的科学计算、`Matplotlib`负责数据可视化的操作，三者并成为Python数据分析界的三大剑客。接下来，我们从Numpy出发，开始入门数据分析三剑客。

## 1.Numpy库

Numpy是一个运行速度非常快的数学库，主要用于数组计算。它包含一个强大的N维数组对象，拥有广播功能函数、整个C/C++/Fortran代码的工具以及线性代数，傅里叶变换，随机数生成等功能。它最重要的一个特点是其N维数组对象`ndarray`，它是一系列同类型数据的集合。

### 1.1创建ndarray的对象

ndarray是一个类，其默认构造函数是`ndarray()`。而array是一个函数，便于创建一个ndarray对象。这里用`.array()`方法创建对象

```python
import numpy as np
# 将python中的列表转换成numpy的矩阵
array = np.array([[1, 2, 3], [4, 5, 6]])
array
```

```python
array([[1, 2, 3],
       [4, 5, 6]])
```

如果有需要把Pandas的`DataFrame`对象转换为ndarray，也可以直接使用`array()`函数:

```py
# 假设已经创建好一个DataFrame对象，其值如下:
print(df.shape)
df
```

<img src="../../Pictures/数据分析/微信截图_20231030141747.png" align="left" style="zoom:40%;" />

```py
# 将这个6行4列的表格转换成numpy当中的矩阵
matrix = np.array(df3)
matrix
```

<img src="../../Pictures/数据分析/微信截图_20231030141912.png" align="left" style="zoom:40%;" />

成功转换成ndarray对象。

### 1.2ndarray的基本属性

- `.ndim`： 输出矩阵的维度
- `.shape`: 输出行行数和列数，返回结果是一个元组
- `.size`: 输出矩阵中元素的数量
- `.dtype`: 输出矩阵的数据类型

```python
import numpy as np
array = np.array([[1, 2, 3], [4, 5, 6]])
print(array)  # 输出矩阵
print(array.ndim)  # 输出维度
print(array.shape)  # 输出行数和列数
print(array.size)  # 输出元素数量
```

```python
[[1 2 3]
 [4 5 6]]
2
(2, 3)
6
```

在Numpy当中，数据类型对象叫做`dtype`，`d`即维度(*`dimension`*)，常见的`dtype`有`int32`、`int64`、`float32`和`float64`，其中数字代表它们的精度。由于它们都是Numpy中新增加的数据类型，故如果需要手动修改数据类型，还需要通过Numpy的对象名`np`来调用：

```py
a = np.array([2, 4, 6], dtype=np.int64)
print(a.dtype)  # int64
```



> 注意array矩阵的元素使用空格分隔，而Python当中不同元素使用逗号分隔。

### 1.3不同的ndarray对象

- **创建一维数组**

```python
import numpy as np
a = np.array([2, 4, 6])
print(a)
```

```python
[2 4 6]
```

- **创建零矩阵**

```python
a = np.zeros(shape=(3, 4))  # 定义为3行4列
print(a)
```

```python
[[0. 0. 0. 0.]
 [0. 0. 0. 0.]
 [0. 0. 0. 0.]]
```

- **创建全部为1的矩阵**

`ones()`函数返回给定形状和数据类型的新数组，其中元素的值设置为1。此函数与`zeros()`函数非常相似。

```py
a = np.ones(shape=(3, 4)) # 创建3行4列的矩阵，其元素填充为1
print(a.dtype)  # 查看矩阵的数据类型
a
```

<img src="../../Pictures/数据分析/微信截图_20231030144103.png" align="left" style="zoom:40%;" />

可看到该矩阵的数据类型是`float64`。如果需要该矩阵的数据类型为整型，可以这样定义：

```py
a = np.ones(shape=(3, 4), dtype=np.int16)  # 定义为3行4列
a
```

<img src="../../Pictures/数据分析/微信截图_20231030144339.png" align="left" style="zoom:40%;" />

**创建空矩阵**

```py
a = np.empty((3, 4))
print(a)
```

```python
[[0. 0. 0. 0.]
 [0. 0. 0. 0.]
 [0. 0. 0. 0.]]
```

> 该矩阵的每个元素都是非常接近0的元素。

**创建有序序列**

使用`np.arange()`函数：

```py
a = np.arange(10, 20, 2)  # arange用法与python中range的用法一致
print(a)
```

```py
[10 12 14 16 18]
```

**创建有序矩阵**

使用`.reshape()`函数，需要传入一个二元组，包括该矩阵的行和列长度：

```py
# 创建一个3行4列，元素从0到11的矩阵
a = np.arange(12).reshape((3, 4))
print(a)
```

```py
[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]]
```

**创建一条线段**

使用`linspace()`函数，生成一个指定大小，指定数据区间的均匀分布序列。其原型如下：

```py
.linspace(start, stop, num=50, endpoint=True, retstep=False, dtype=None)
```

常用参数介绍：

- `start`：序列中数据的下界

- `end`：序列中数据的上界

- `num`：生成序列包含num个元素；其值默认为50

- `endpoint`：取True时，序列包含最大值end；否则不包含；其值默认为True

- `retstep`：该值取True时，生成的序列中显示间距；否则不显示；其值默认为False

- `dtype`：数据类型，可以指定生成序列的数据类型；当为None时，根据其他输入推断数据类型



```python
a = np.linspace(1, 10, 6, dtype=np.int16).reshape((2, 3))  # 生成从1开始，到10结束，共6个数的数列(自动匹配步长)
print(a)
```

```py
[[ 1  2  4]
 [ 6  8 10]]
```

**创建随机矩阵**

- **randint**

`random.randint()`函数根据给定范围产生随机整数，其原型如下:

```py
.random.randint(low, high=None, size=None, dtype='l')
```

常用参数介绍:

- `low`: 随机整数的最小值

- `high`: 随机整数的上限(最终产生的数会落在$low\leq x<high$的内)

- `size`: 输出的大小(传入整数n代表创建长度为n的序列，传入元组(a,b)代表创建a行b列的矩阵)

- `dtype`: 期望结果的数据类型

```py
# 创建一个长度为10，范围在[5,40)的随机序列
array = np.random.randint(5, 40, 10)
```

```py
array([30,  6, 15, 35, 39, 38, 32, 29, 26, 37])
```

```py
# 创建一个4行5列，范围在[5,40)的随机矩阵，
A = np.random.randint(5, 40, (4, 5))
```

<img src="../../Pictures/数据分析/微信截图_20231030143232.png" align="left" style="zoom:40%;" />

- **rand**

`rand()`函数根据给定维度生成[0,1)之间的数据，包含0，不包含1:

```py
# 创建一个长度为10的序列
np.random.rand(10)
```

<img src="../../Pictures/数据分析/微信截图_20231031121011.png" align="left" style="zoom:40%;" />

```py
# 创建一个4行2列的随机矩阵
np.random.rand(4,2)
```

<img src="../../Pictures/数据分析/微信截图_20231031120800.png" align="left" style="zoom:40%;" />

- **randn**

`randn()`函数返回一个或一组样本，具有标准正态分布:

```py
np.random.randn() # 当没有参数时，返回单个数据
```

```py
-0.6491720916258932
```

```py
# 创建一个2行4列，矩阵正态分布的随机矩阵
np.random.randn(2,4)
```

<img src="../../Pictures/数据分析/微信截图_20231031121540.png" align="left" style="zoom:40%;" />

- **choice**

`choice()`函数从一个列表中随机抽取k个元素，并返回一个新列表或随机元素(k为1时):

```py
np.random.choice(original_list, k, replace=False)  # replace参数设置为False确保不重复抽取
```

```
list = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
np.random.choice(list, 3, replace=False)
```

<img src="../../Pictures/数据分析/微信截图_20231101200353.png" align="left" style="zoom:40%;" />

### 1.4array的基础运算

**一维数组**

对于一维数组，运算就是对应元素进行运算：

```python
import numpy as np

a = np.array([10, 20, 30, 40])
b = np.arange(4)
# 减法
c = a - b
print(a, b)
print(c)
print("=" * 10)
# 加法
c = a + b
print(c)
print("=" * 10)
# 乘法
c = a * b
print(c)
print("=" * 10)
```

```python
[10 20 30 40] [0 1 2 3]
[10 19 28 37]
==========
[10 21 32 43]
==========
[  0  20  60 120]
==========
```

**其他运算**

```py
c = 10 * np.sin(a)  # 正弦
print(c)
print("=" * 10)
# 筛选
b = np.arange(4)
print(b)
print(b < 3)  # 返回一个列表，该列表对应原数组该条件的满足情况
print("=" * 10)
```

```py
[-5.44021111  9.12945251 -9.88031624  7.4511316 ]
==========
[0 1 2 3]
[ True  True  True False]
==========
```

**矩阵**

```py
a = np.array([[1, 1], [0, 1]])
b = np.arange(4).reshape((2, 2))
print(a)
print(b)
```

```py
[[1 1]
 [0 1]]
[[0 1]
 [2 3]]
```

**矩阵中元素对应相乘(数乘)**

```py
c = a * b
print(c)
print("=" * 10)
```

```py
[[0 1]
 [0 3]]
==========
```

**矩阵中的乘法(点乘)**

```py
c = np.dot(a, b)
print(c)
print("=" * 10)
# 等价为
c = a.dot(b)
print(c)
print("=" * 10)
```

```py
[[2 4]
 [2 3]]
==========
[[2 4]
 [2 3]]
==========
```

**常用运算1**

```py
# 查找最值、平均值、求和
a = np.random.random((2, 4))  # 随机生成2行4列的矩阵
print(a)
print(np.sum(a))
print(np.min(a))
print(np.max(a))
print(np.average(a))
print("=" * 10)
```

```py
[[0.32178851 0.36945906 0.47043426 0.97250985]
 [0.40558691 0.91389345 0.58745997 0.60485456]]
4.64598655147112
0.32178850886343635
0.9725098455008124
0.58074831893389
==========
```

如果只需要对行或者列进行上述运算，则可以指定`axis`。其中`axis=0`表示对行求和，`axis=1`对列求和，结果返回一个数组或矩阵。

```py
print(np.sum(a, axis=1))  # axis=0对行进行求和，axis=1对列求和，结果返回一个数组或矩阵
```

```py
[2.13419167 2.51179488]
```

**常用运算2**

```py
import numpy as np
A = np.arange(2, 14).reshape((3, 4))
print(A)
```

```py
[[ 2  3  4  5]
 [ 6  7  8  9]
 [10 11 12 13]]
```

**查找索引**

```py
# 寻找最小值索引
print(np.argmin(A))
# 寻找最大值索引
print(np.argmax(A))
print("=" * 10)
```

```py
0
11
==========
```

**计算平均值**

```py
print(np.mean(A))  # 或np.average(A)
# 等价于
print(A.mean())
print("=" * 10)
```

```py
7.5
7.5
==========
```

**计算中位数**

```py
print(np.median(A))
print("=" * 10)
```

```py
7.5
==========
```

**累加**

```py
# 返回一个数组，数组中第n个数的值对应矩阵中前n个数相加
print(np.cumsum(A))  
```

```py
[ 2  5  9 14 20 27 35 44 54 65 77 90]
```

**累差**

```py
# 返回一个新矩阵，矩阵中某一元素等于原矩阵中后一个元素减前一个元素的差值
print(np.diff(A))  
print("=" * 10)
```

```py
[[1 1 1]
 [1 1 1]
 [1 1 1]]
==========
```

**查找非零数**

 返回两个数组，第一个数组代表原矩阵的每一行，第二个数组代表原矩阵的每一列，两个数组对应看即可查找到原矩阵中非零项元素

```py
print(list(np.nonzero(A)))  
print("=" * 10)
```

```py
[array([0, 0, 0, 0, 1, 1, 1, 1, 2, 2, 2, 2], dtype=int64), array([0, 1, 2, 3, 0, 1, 2, 3, 0, 1, 2, 3], dtype=int64)]
==========
```

**矩阵的转置**

```py
print(np.transpose(A))
# 等效于
print(A.T)
print("=" * 10)
```

```py
[[14 10  6]
 [13  9  5]
 [12  8  4]
 [11  7  3]]
[[14 10  6]
 [13  9  5]
 [12  8  4]
 [11  7  3]]
==========
```

**截取矩阵**

```py
print(np.clip(A, 5, 9))  # 所有小于5的数都使其等于5，所有大于9的数都使其等于9，在5和9之前的数不变
```

```py
[[9 9 9 9]
 [9 9 8 7]
 [6 5 5 5]]
```

**计算行或列的平均值**

```py
A = np.arange(14, 2, -1).reshape((3, 4))
print(A)
print(np.mean(A, axis=1))  # 计算行的平均值
print(np.mean(A, axis=0))  # 计算列的平均值
```

```py
[12.5  8.5  4.5]
[10.  9.  8.  7.]
```

### 1.5通过索引访问元素

```py
# 对于一维数组数组
A = np.arange(3, 15)
print(A)
# 根据索引访问元素
print(A[3])
```

```py
[ 3  4  5  6  7  8  9 10 11 12 13 14]
6
```

**根据一级索引访问行**

```py
# 对于矩阵
A = np.arange(3, 15).reshape((3, 4))
print(A)
print(A[2])
# 等效于
print(A[2, :])  
```

`[ ]`中可以写入两个整数，逗号前表示行，逗号后表示列；`':'`表示匹配某一行或某一列的所有书

```py
[[ 3  4  5  6]
 [ 7  8  9 10]
 [11 12 13 14]]
[11 12 13 14]
[11 12 13 14]
```

**两个索引确定要访问的元素**

```py
print(A[1][1])
# 等效于
print(A[1, 1])
```

```py
8
8
```

**访问连续的几个数**

```py
print(A[1, 1:3])  # 访问第一行的第2、3个数
```

```py
[8 9]
```

**与for循环有关的遍历**

```py
# for循环遍历每一个元素
print(A.flatten())  # 将矩阵A变成一个一维数组
for item in A.flat:  # flat是一个迭代器，flatten()是将矩阵变为一维数组
    print(item, end=" ")
print()
print("=" * 10)
# for循环迭代行
for row in A:
    print(row)
print("=" * 10)
# for循环迭代列
for column in A.T:  # 通过转置实现
    print(column)
```

```py
[ 3  4  5  6  7  8  9 10 11 12 13 14]
3 4 5 6 7 8 9 10 11 12 13 14 
==========
[3 4 5 6]
[ 7  8  9 10]
[11 12 13 14]
==========
[ 3  7 11]
[ 4  8 12]
[ 5  9 13]
[ 6 10 14]
```

### 1.6合并array

准备好两个序列

```py
import numpy as np
A = np.array([1, 1, 1])
B = np.array([2, 2, 2])
```

**进行上下合并**

使用`vstack()`函数(*`vertical stack`*)垂直堆叠，输入的参数应该为一个元组对象，包括需要合并的array对象：

```py
C = np.vstack((A, B))
print(C)
print(C.shape)
```

```py
[[1 1 1]
 [2 2 2]]
(2, 3)
```

**左右合并**

使用`hstack()`函数(*`horizontal stack`*)水平堆叠:

```py
D = np.hstack((A, B))
print(D)
print(D.shape)
print("=" * 10)
```

```py
[1 1 1 2 2 2]
(6,)
==========
```

**将一维数组转换成列数为1的矩阵**

使用`newaxis`属性，在`[ , ]`逗号左侧代表给行新增一个维度，逗号右侧代表给列新增一个维度:

```py
print(A[np.newaxis, :])  # 给行新增一个维度
print(A[:, np.newaxis])  # 给列新增一个维度
A = A[:, np.newaxis]
B = B[:, np.newaxis]
# 对修改后的A,B进行左右合并
D = np.hstack((A, B))
print(D)
print("=" * 10)
```

```py
[[1 1 1]]
[[1]
 [1]
 [1]]
[[1 2]
 [1 2]
 [1 2]]
==========
```

**多个array进行纵向或横向合并:**

使用`concatenate()`函数，传入的参数有一个元组`tup`，里面包括需要合并的array对象，以及合并的方向`axis`:

```py
C = np.concatenate((A, B, B, A), axis=0)  # 0表示上下合并，1表示左右合并
print(C)
C = np.concatenate((A, B, B, A), axis=1)
print(C)
```

```py
[[1]
 [1]
 [1]
 [2]
 [2]
 [2]
 [2]
 [2]
 [2]
 [1]
 [1]
 [1]]

[[1 2 2 1]
 [1 2 2 1]
 [1 2 2 1]]
```

### 1.7分割array

```py
import numpy as np
A = np.arange(12).reshape((3, 4))
print(A)
```

```py
[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]]
```

分割时需要用到`split()`函数，其原型如下：

```py
.split(ary, indices_or_sections, axis=0)
```

常用参数介绍：

- `ary`: 要切分的array对象 
- `indices_or_sections`: 要切分成几份；如果是一个整数，就用该数平均切分，如果是一个数组，为沿轴切分的位置（左开右闭） 
- `axis`： 沿着哪个维度进行切向，默认为0，横向切分；为1时，纵向切分

**纵向分割**

```py
print(np.split(A, 2, axis=1))  # 按列进行分割，分割成2列
print("=" * 10)
```

```py
[array([[0, 1],
       [4, 5],
       [8, 9]]), array([[ 2,  3],
       [ 6,  7],
       [10, 11]])]
==========
```

**横向分割**

```py
print(np.split(A, 3, axis=0))
print("=" * 10)
```

```py
[array([[0, 1, 2, 3]]), array([[4, 5, 6, 7]]), array([[ 8,  9, 10, 11]])]
==========
```

**不等样分割**

使用`split()`函数只能进行均等分割，否则会报错；如果需要进行不均等分割，需要用到`array_split()`函数:

```py
print(np.array_split(A, 3, axis=1)) 
```

```py
[array([[0, 1],
       [4, 5],
       [8, 9]]), array([[ 2],
       [ 6],
       [10]]), array([[ 3],
       [ 7],
       [11]])]
```

**另一种方法实现不等样分割**

另外，和合并时类似，可以通过指定`vertical`或`horizontal`的方式进行切割；这种方法不需要再传入`axis`参数:

```py
print(np.vsplit(A, 3))  # 纵向分割
print(np.hsplit(A, 2))  # 横向分割
print("=" * 10)
```

```py
[array([[0, 1, 2, 3]]), array([[4, 5, 6, 7]]), array([[ 8,  9, 10, 11]])]
[array([[0, 1],
       [4, 5],
       [8, 9]]), array([[ 2,  3],
       [ 6,  7],
       [10, 11]])]
==========
```

### 1.8复制array

```py
import numpy as np
a = np.arange(4)
print(a)
```

```py
[0 1 2 3]
```

**浅拷贝**

直接通过等号`'='`复制

```py
b = a
a[0] = 11
print(a)
print(b)
```

```
[11  1  2  3]
[11  1  2  3]
```

尝试修改b的值

```py
b[1:3] = [22, 33]
# 查看a的值是否会被修改
print(a)  # 
```

```py
[11 22 33  3]
```

发现a的值也随之被修改。发现a和b是相关联的，即a就是b。如果希望a和b不关联，则需要进行深拷贝。

**深拷贝**

```py
b = a.copy()  # 将a的值赋给b，但二者并不关联
a[3] = 44
print(a)
print(b)
```

```py
[11 22 33 44]
[11 22 33  3]
```

发现a、b不再关联。

## 2.Pandas库

`Pandas`是基于`NumPy`的一种工具，该工具是为解决数据分析任务而创建的。`Pandas`纳入了大量库和一些标准的数据模型，提供了高效地操作大型数据集所需的工具。此外，它还提供了大量能使我们快速便捷地处理数据的函数和方法。

### 2.1创建一个序列

#### 2.1.1Series对象

`Series`是Pandas库中的一组数据结构，类似于一维数组，类由一组数据以及与这组数据有关的标签(索引)组成。原型为：

```py
.Series(data=None, index=None, dtype=None, name=None, copy=False, fastpath=False)
```

常用参数介绍：

- `data`: 需要处理的序列
- `index`: 指定索引名称
- `dtype`: 数据类型

```py
import pandas as pd
import numpy as np
s= pd.Series([1,3,6,np.nan,44,1])  #传入一个序列，其中nan表示为空
print(s)
```

```py
0     1.0
1     3.0
2     6.0
3     NaN
4    44.0
5     1.0
dtype: float64
```

#### 2.1.2date_range对象

date_range()是Pandas中常用的函数，用于生成一个固定频率的`DatetimeIndex`时间索引，其原型为：

```py
.date_range(start=None, end=None, periods=None, freq=None, tz=None, normalize=False, name=None, closed=None, **kwargs)
```

常用参数介绍：

- `start`： 指定生成时间序列的开始时间(基础格式为`'YYYY(年)mm(月)dd(日)'`，如'20220101'将会被识别成'2022-01-01')
- `end`： 指定生成时间序列的结束时间
- `periods`： 指定生成时间序列的数量

```py
# 生成一个从1月1日到1月6日的日期序列
dates=pd.date_range('20220101',periods=6)
print(dates)
```

```py
DatetimeIndex(['2022-01-01', '2022-01-02', '2022-01-03', '2022-01-04',
               '2022-01-05', '2022-01-06'],
              dtype='datetime64[ns]', freq='D')
```

### 2.2创建DataFrame的对象

`DataFrame`对象也是Pandas库中的一种数据结构，类似于二维表，由行和列组成。与Series一样支持多种数据类型：

```python
DataFrame(data=None,index=None,columns=None,dtype=None)
```

常用参数介绍

- `data`: 需要处理的数据


- `index`: 行索引标签


- `columns`: 列索引标签


- `dtype`: 数据类型

#### 2.2.1Numpy提供数据源

*`i)`* **data的数据来源可以来自numpy：**

```py
df = pd.DataFrame(
    np.random.randn(6, 4), index=dates, columns=["a", "b", "c", "d"]
)  # 数据源由numpy的random函数随机生成
df
```

<img src="../../Pictures/数据分析/微信截图_20231029190237.png" align="left" style="zoom:40%;" />

```py
# 使用默认行索引和列索引
df1 = pd.DataFrame(np.arange(12).reshape((3, 4)))
df1
```

<img src="../../Pictures/数据分析/微信截图_20231029190555.png"  align="left" style="zoom:40%;" />

#### 2.2.2字典匹配数据

*`ii)`* **可以来自字典：**

```py
df2 = pd.DataFrame(
    {
        # value可以是pandas的series对象或者numpy的array对象或者其他形式的序列
        "A": 1.0,
        "B": pd.Timestamp("20130302"),
        "C": pd.Series(1, index=list(range(4)), dtype="float32"),
        "D": np.array([3] * 4, dtype="int32"),
        "E": pd.Categorical(["test", "train", "test", "train"]),
        "F": "foo",
    }
)
df2
```

<img src="../../Pictures/数据分析/微信截图_20231029190906.png" align="left" style="zoom:40%;" />

> 当value只有一个值是，默认将这个值填充至整一列。

#### 2.2.3Python列表创建

*`iii)`* **可以来自Python的列表:**

```py
data = [["Tifa", 100, "F"], ["Cloud", 80, "M"], ["Aerith", 95, "F"]]
columns = ["名字", "成绩", "性别"]
df3 = pd.DataFrame(data=data, columns=columns)
df3
```

<img src="../../Pictures/数据分析/微信截图_20231029191508.png" align="left" style="zoom:40%;" />

### 2.3DataFrame的基本属性

- `values` 查看所有元素的值

- `dtypes` 查看所有元素的类型

- `index` 查看所有行名、重命名行名

- `columns` 查看所有列名、重命名列名

- `T` 行列数据转换

- `head` 查看前N条数据，默认5条

- `tail` 查看后N条数据，默认5条

- `shape` 查看行数和列数；shape[0]表示行，shape[1]表示列

- `info` 查看索引、数据类型和内存信息

以`df2`为例：

```py
# 返回数据类型
df2.dtypes  # Index([0, 1, 2, 3], dtype='int64')
# 返回行的索引
df2.index  # Index([0, 1, 2, 3], dtype='int64')
# 返回列的索引
df2.columns  # Index(['A', 'B', 'C', 'D', 'E', 'F'], dtype='object')
# 返回所有的values
df2.values
```

<img src="../../Pictures/数据分析/微信截图_20231029192006.png" align="left" style="zoom:40%;" />

```py
df2.T
```

<img src="../../Pictures/数据分析/微信截图_20231029193525.png" align="left" style="zoom:40%;" />

### 2.4统计变量和排序

**describe()**

上面已经了解到Pandas有两个核心数据结构`Series`和`DataFrame`，分别对应了一维的序列和二维的表结构。而describe()函数就是返回这两个核心数据结构的统计变量。继续以df2为例：

```py
# 描述方差、平均值等
df2.describe()
```

<img src="../../Pictures/数据分析/微信截图_20231029192502.png" align="left" style="zoom:40%;" />

> 缺失值由NaN补上，如果为NaN，说明此列的信息不可以用这个统计变量进行统计的。

统计值变量说明：

-    `count`：数量统计，此列共有多少有效值
-    `std`：标准差
-    `min`：最小值
-    `25%`：四分之一分位数
-    `50%`：二分之一分位数
-    `75%`：四分之三分位数
-    `max`：最大值
-    `mean`：均值

**sort_index()**

`sort_index()`用来按索引排序，其原型为：

```py
.sort_index(axis=0, level=None, ascending=True, inplace=False, kind=‘quicksort’, na_position=‘last’,sort_remaining=True)
```

常用参数介绍：

上述方法中常用参数：

- `axis`：轴索引（排序的方向），0表示按行，1表示按列

- `level`：若不为None，则对指定索引级别的值进行排序

- `ascending`：是否升序排列，默认为True，表示升序

- `inplace`：默认为False，表示对数据表进行排序，不创建新的实例

- `kind`：选择排序算法

```py
df2.sort_index(axis=1, ascending=False)  # 按列排序，打开降序
```

<img src="../../Pictures/数据分析/微信截图_20231029193245.png" align="left" style="zoom:40%;" />

```py
df2.sort_index(axis=0, ascending=False)  # 按照行排序，打开降序
```

<img src="../../Pictures/数据分析/微信截图_20231029193406.png" align="left" style="zoom:40%;" />

对某一个列的元素进行排序

```py
df2.sort_values(by="E")
```

<img src="../../Pictures/数据分析/微信截图_20231029193746.png" align="left" style="zoom:40%;" />

### 2.5导入外部数据

#### 2.5.1导入本地文件

- **导入.xls或.xlsx文件**

使用`read_excel()`函数，其原型如下:

```python
.read_excel(io,sheet_name = 0,header = 0,names = None,usecols = None,dtype = None,skiprows=None,nrows=None)
```

常用参数说明:

- `io`: `xls`或者`xlsx`的文件路径或类文件对象


- `sheet_name`: 表示工作表，取值如下表所示


- `header`: 默认值为0，取第一行的值为列名，数据为除列名以外的数据，如果数据不包含列名，则设置`header=None`
- `usecols`: 指定读取某一列或多列，参数需要传递一个列表
- `skiprows`: 用于跳过特定的函数，参数传递一个列表
- `nrows`: 用于读取前n行的数据


| 值                          | 说明                                                         |
| --------------------------- | ------------------------------------------------------------ |
| `sheet_name=0`              | 第一个`Sheet`页中的数据作为DataFrame对象                     |
| `sheet_name=1`              | 第二个`Sheet`页中的数据作为DataFrame对象                     |
| `sheet_name='Sheet1'`       | 名称为`Sheet1`的`Sheet`页中的数据作为DataFrame对象           |
| `sheet_name=[0,1,'Sheet3']` | 第一个、第二个和名称为`Sheet3`的`Sheet`页中的数据作为DataFrame对象 |
| `sheet_name=None`           | 读取所有工作表                                               |

```python
import pandas as pd
df = pd.read_excel('xxx.xlsx',sheet_name=1,header=None)
```

导入指定列的数据

```python
import pandas as pd
df = pd.read_excel('xxx.xlsx',sheet_name=3,usecols=[1])  # 只读取第二列的数据(通过索引或首列名称)
```

导入多列的数据

```python
import pandas as pd
df = pd.read_excel('xxx.xlsx',sheet_name=3,usecols=[0,1])  # 只读取第一和第二列的数据
```

- **导入csv文件**

csv文件与xlsx文件相似，可以自定义分隔符，能从记事本打开。导入csv文件使用`read_csv()`函数，其原型如下:

```python
.read_csv(filepath_or_buffer,sep=',',header,encoding=None)
```

常用参数说明:

- `filepath_or_buffer`：字符串、文件路径，也可以是URL链接


- `sep`：字符串、分隔符


- `header`：指定作为列名的行，默认为0，即取第一行的值为列名。数据为除列名以外的数据，若数据不包含列表，则设置为`header=None`


- `encoding`：字符串、默认值为None，文件的编码格式(可以从记事本中查看)


```python
import pandas as pd
df = pd.read_csv('xxx.csv',sep=',',encoding='gbk')
df.head()  # 输出前5条数据
```

- **导入txt文件**

```python
.read_txt(filepath_or_buffer,sep='\t',header,encoding=None)
```

#### 2.5.2导入html文件

```python
.read_html(io,match='.+',flavor,header,encoding)
```

常用参数说明:

- `io`：字符串、文件路径，可以是URL链接


- `match`：正则表达式


- `flavor`：解释器默认为lxml


- `header`：指定列标题所在的行


- `encoding`：文件的编码格式


```python
import pandas as pd
url = 'https://zhuanlan.zhihu.com/p/472053977'
df = pd.DataFrame()  # 创建一个空的DataFrame对象
# DataFrame添加数据
df = df._append(pd.read_html(url,header=0))
df
```

<img src="../../Pictures/数据分析/微信截图_20231029194533.png" align="left" style="zoom:40%;" />

如果网页上存在多张表格，那么该函数会按照它们的出现顺序把表格存放到一个列表当中；列表中每一个元素都对应一个表格。

> 注意，使用该函数只能导入网页当中含有`<table>`标签的数据，其他的无法读取。

### 2.6数据提取

```py
import numpy as np
import pandas as pd

dates = pd.date_range("20220101", periods=6)
df = pd.DataFrame(
    # 创建一张6行4列的表
    np.arange(24).reshape((6, 4)), index=dates, columns=["A", "B", "C", "D"]
)
df
```

<img src="../../Pictures/数据分析/微信截图_20231029194842.png" align="left" style="zoom:40%;" />

#### 2.6.1访问指定行或列

Pandas查询数据有很多种方式，比较常见的有`df[ ]`形式，`df.A`属性方式，`df.iloc[]`方式和`df.loc[]`方式。

- **获取某一列数据**

通过`df[标签名]`访问。`df[ ]`索引方式仅接收一个参数，对于获取整行整列的数据十分方便。*注意，使用`['label']`字符串形式仅接收**列标签***。

```py
print(df["A"])  # 获取列名为'A'的一列
```

```py
2022-01-01     0
2022-01-02     4
2022-01-03     8
2022-01-04    12
2022-01-05    16
2022-01-06    20
Freq: D, Name: A, dtype: int32
```

> 另外，如果`[ ]`当中是一个列表`['label1'，'label2'[，...]]`，则列表中的元素必须是列标识。简单地说，就是利用`df[ ]`形式时，如果里面的数据是(一个或多个)标签的话，只允许是列标签。		
>

- **获取连续的行或列的数据**

通过切片来访问。**使用切片形式的话，必须是行标签或者行索引**:

```py
print(df[0:3])  # 获取第一行到第四行的所有数据
# 等效于
print(df["20220101":"20220103"])
```

```py
# 运行结果一致
A  B   C   D
2022-01-01  0  1   2   3
2022-01-02  4  5   6   7
2022-01-03  8  9  10  11
```

> *注意，使用位置索引包头不包尾，使用标签索引包头又包尾。*



另外，还可以通过`.loc[ ]`和`.iloc[ ]`属性访问到元素，二者的区别在于前者通过标签选择，后者通过位置索引选择。无论是`loc`还是`iloc`，在`[ ]`内可以写入一个或两个整数(或者是列表)，中间用逗号分隔，逗号前表示行，逗号后表示列。例如，`[num]`或者`['str']`代表查询某一行，`[:,num]`或者`[:,'str']`代表查询某一列。另外，如果是写入列表的话，表示匹配多个行或列。

- **使用标签选择某一行：**

通过`loc`访问：

```py
print(df.loc["20220102"])
# 等效于
print(df.loc["20220102", :]) 
```

```py
# 运行结果一致
A    4
B    5
C    6
D    7
Name: 2022-01-02 00:00:00, dtype: int32
```

- **使用位置选择某一行:**

通过`iloc`访问：

```py
print(df.iloc[3])  # 查看第四行
# 通过两个位置定位一个元素
print(df.iloc[3, 1])  # 查看第四行第二位数
# 定位连续的多个元素
print(df.iloc[3:5, 1:3])  # 查看第四行到第五行，第二列到第三列之间的元素
# 定位不连续的多个元素
print(df.iloc[[1, 3, 5], 1:3])
```

```py
A    12
B    13
C    14
D    15
Name: 2022-01-04 00:00:00, dtype: int32

13
             B   C
2022-01-04  13  14
2022-01-05  17  18

             B   C
2022-01-02   5   6
2022-01-04  13  14
2022-01-06  21  22
```



​	除了使用`df.loc(iloc)`或者`df[ ]`来查询行或列的数据外，如果只需要查询某一列的数据，`Pandas`还提供了一个更简洁的属性，即`df.列名`直接获取该列的数据。

> *注意，如果使用`df.列名`的方法，该标签名只能是**字符串(或单个字符)形式(允许接收中文和英文，但不能是数字、符号)**，不能是其他形式。*

```py
import numpy as np
import pandas as pd

data = np.arange(12).reshape((3, 4))
columns = ["第一列", "b", "third", 4]
df = pd.DataFrame(data=data, columns=columns, index=[1, 2, 3])
df
```

<img src="../../Pictures/数据分析/微信截图_20231030113742.png" align="left" style="zoom:40%;" />

```py
# 尝试获取第一列数据
df.第一列
```

```py
# 成功运行
1    0
2    4
3    8
Name: 第一列, dtype: int32
```

```py
#尝试获取第二列数据
df.b
```

```py
# 成功运行
1    1
2    5
3    9
Name: b, dtype: int32
```

```py
#尝试获取第三列数据
df.third
```

```py
# 成功运行
1     2
2     6
3    10
Name: third, dtype: int32
```

```py
#尝试获取第四列数据
df.4
```

```py
# 获取失败
 Cell In[5], line 1
    df.4
      ^
SyntaxError: invalid syntax
```

也就是说，当只需要查询某一列的数据，且该列的列名是一个不包含浮点和数字的中文或英文字符串时，可以使用`df.列标签名`的方法。

#### 2.6.2通过条件判断访问

```py
data = np.arange(24).reshape((6, 4))
index = pd.date_range("20200101", periods=6)
columns = ["A", "B", "C", "D"]
df = pd.DataFrame(data=data, index=index, columns=columns)
df
```

<img src="../../Pictures/数据分析/微信截图_20231029200607.png" align="left" style="zoom:40%;" />

```py
# 查看列名为'A'的列元素值大于8的元素
df[df.A > 8]  
# 等效于
df[df['A'] > 8]
```

<img src="../../Pictures/数据分析/微信截图_20231029200805.png" align="left" style="zoom:40%;" />

> *注意，只要该列的行数被确定下来，其他列的行数会保持和这个列一致。*

### 2.7数据处理

#### 2.7.1修改元素及行列名

**根据位置修改：**

```py
df.iloc[2, 2] = 1111 
df
```

<img src="../../Pictures/数据分析/微信截图_20231029201045.png" align="left" style="zoom:40%;" />

**根据标签修改:**

```py
df.loc["20220101", "B"] = 2222
df
```

<img src="../../Pictures/数据分析/微信截图_20231029201236.png" align="left" style="zoom:40%;" />

**根据条件修改:**

观察以下代码:

```py
# 尝试将列名为'A'的列所有大于8的元素都替换为0
df[df.A > 8] = 0
df
```

<img src="../../Pictures/数据分析/微信截图_20231030115541.png" align="left" style="zoom:40%;" />

发现不仅仅是A列满足情况的元素被替修改了，并且和它们同一行的其他列的元素也随之被修改了。为了避免类似情况，修改对代码进行调整:

```py
# 需要调用两次A
df.A[df.A > 4] = 0  
df
```

<img src="../../Pictures/数据分析/微信截图_20231029201431.png" align="left" style="zoom:40%;" />

**修改标题:**

使用`columns`属性修改列标题:

```py
import pandas as pd

pd.set_option("display.unicode.east_asian_width", True)
data = [[45, 65, 100], [56, 45, 50], [67, 67, 76]]
index = ["Tifa", "Cloud", "Aerith"]
df = pd.DataFrame(data=data, index=index)
df
```

<img src="../../Pictures/数据分析/微信截图_20231029205459.png" align="left" style="zoom:40%;" />

```py
df.columns = ["HP", "MP", "AP"]
df
```

<img src="../../Pictures/数据分析/微信截图_20231029205609.png" align="left" style="zoom:40%;" />

使用`index`属性修改列标题:

```py
df.index = [1, 2, 3]
```

<img src="../../Pictures/数据分析/微信截图_20231029205805.png" align="left" style="zoom:40%;" />

使用`rename()`函数修改:

```py
df.rename(
    # 使用字典的形式，原名、修改后的名称进行匹配
    columns={"HP": "AP", "MP": "HP", "AP": "MP"},
    index={1: "Zack", 2: "Red VIII", 3: "Cloud"}
) 
```

<img src="../../Pictures/数据分析/微信截图_20231029210315.png" align="left" style="zoom:40%;" />

#### 2.7.2新增行列

新增列可以使用`df[ ]`或者`df.loc[ ]`来实现。有时新增的数据可能与原表中的数据数据类型不兼容，Pandas会默认转换表格的数据类型，最常见的就是`int`转换成`float`，但有时也会错误地转换。如果不希望这类情况发生，可以使用`astype()`函数强制转换数据的类型。

**通过numpy初始化:**

```py
# 新增一列并初始化
df["E"] = np.nan
df
```

<img src="../../Pictures/数据分析/微信截图_20231029202407.png" align="left" style="zoom:40%;" />

**通过列表初始化:**

```py
# 使用列表初始化时，元素默认对齐表格
df['F']=[4,5,23,6,49,11]
df
```

<img src="../../Pictures/数据分析/微信截图_20231029202446.png" align="left" style="zoom:40%;" />

**通过pandas初始化:**

```py
df["G"] = pd.Series(
    # 索引要与原表格的一致，这样才能与原表格对齐
    [1, 2, 3, 4, 5, 6], index=pd.date_range("20220101", periods=6)
)  
df
```

<img src="../../Pictures/数据分析/微信截图_20231029202553.png" align="left" style="zoom:40%;" />

除了使用`df[ ]`属性外，还可以使用`loc[ ]`新增一列:

```py
data = np.arange(24).reshape((6, 4))
index = pd.date_range("20200101", periods=6)
columns = ["A", "B", "C", "D"]
df = pd.DataFrame(data=data, index=index, columns=columns)
df.loc[:,"E"]=pd.Series([1,3,6,2,7,9],index=pd.date_range('20200101',periods=6))
# 等效于 df['E']=pd.Series([1,3,6,2,7,9],index=pd.date_range('20200101',periods=6))
df
```

<img src="../../Pictures/数据分析/微信截图_20231030120922.png" align="left" style="zoom:40%;" />

另外的`df.列标签`和`df.iloc[ ]`不可用于新增列。

同理，新增一行时还是使用`.loc[ ]`实现:

```py
data = np.arange(24).reshape((6, 4))
index = pd.date_range("20200101", periods=6)
columns = ["A", "B", "C", "D"]
df = pd.DataFrame(data=data, index=index, columns=columns)
df
```

<img src="../../Pictures/数据分析/微信截图_20231030122505.png" align="left" style="zoom:40%;" />

**新增一行**

```py
df.loc['2020-01-07',:] = [17,3,42,71]
# 等效于
df.loc['2020-01-07',:] = pd.Series([17,3,42,71],dtype=np.int32,index=columns)
df = df.astype(np.int32)  # 保持数据类型是int32
df
```

<img src="../../Pictures/数据分析/微信截图_20231030122744.png" align="left" style="zoom:40%;" />

#### 2.7.3删除行列

通过`drop()`函数删除某行或某列数据，其原型如下:

```python
.drop(labels=None,axis=0,index=None,columns=None,inplace=False)
```

常用参数介绍：

- `label`: 行标签或列标签

- `axis`: 等于0按行删除，等于1按列删除

- `index`: 删除行(按行标签名删除)，默认值为None

- `columns`: 删除列(按列标签名删除)，默认值为None

- `inplace`: 对原数组做出修改并返回一个新数组；默认值为False，如果值为True，原数组直接被替换

```py
import pandas as pd
pd.set_option("display.unicode.east_asian_width", True)
data = [[45, 65, 100], [56, 45, 50], [67, 67, 76]]
index = ["Tifa", "Cloud", "Aerith"]
columns = ["HP", "MP", "AP"]
df = pd.DataFrame(data=data, index=index, columns=columns)
df
```

<img src="../../Pictures/数据分析/微信截图_20231029203255.png" align="left" style="zoom:40%;" />

**直接删除:**

```py
# 删除行名为'Cloud'的数据
df.drop("Cloud", axis=0)
# 等效于
df.drop(index="Cloud")
```

<img src="../../Pictures/数据分析/微信截图_20231029203335.png" align="left" style="zoom:40%;" />

> 当已经指明是删除行`index`还是列`columns`时，不需要添加参数`axis`。

**通过标签删除:**

```py
df.drop(labels="Aerith", axis=0)
```

<img src="../../Pictures/数据分析/微信截图_20231029203811.png" align="left" style="zoom:40%;" />

> 注意，关键字参数`index=`和`columns=`的实参都应该是标签名，而不是索引值。

**带条件地删除数据:**

在前面的学习中，我们已经知道可以通过对某一列进行条件判断得到一个关于每个行关于这个条件的真假值列表，如:

```py
import pandas as pd
pd.set_option("display.unicode.east_asian_width", True)
data = [[45, 65, 100], [56, 45, 50], [67, 67, 76]]
index = ["Tifa", "Cloud", "Aerith"]
columns = ["HP", "MP", "AP"]
df = pd.DataFrame(data=data, index=index, columns=columns)
df
```

<img src="../../Pictures/数据分析/微信截图_20231030152504.png" align="left" style="zoom:40%;" />

```py
# 查看 HP<60 的满足情况
df["HP"] < 60
```

<img src="../../Pictures/数据分析/微信截图_20231030152611.png" align="left" style="zoom:40%;" />

如果我们想要查看筛选后的表格，还需要在外围嵌套一层`df`，即

```py
df[df["HP"] < 60]
```

<img src="../../Pictures/数据分析/微信截图_20231030152744.png" align="left" style="zoom:40%;" />

如果我们需要把满足条件的元素删除，还需要通过筛选后的表格调用`.index`方法获取到它们的行索引信息:

```py
df[df["HP"] < 60].index
```

```
Index(['Tifa', 'Cloud'], dtype='object')
```

最后把这个整体传入`.drop()`函数即可完成删除:

```py
df.drop(df[df["HP"] < 60].index)  # 删除列名为'HP',且值小于60的行
```

<img src="../../Pictures/数据分析/微信截图_20231029204434.png" align="left" style="zoom:40%;" />

## 3.Matplotlib库

`Matplotlib`是一个Python的2D绘图库，利用它可以画出许多高质量的图像。`Matplotlib`是可视化的表达，在图形的绘制前会涉及一些数据处理，而`Pandas`和`Numpy`则是Python中最好用的两个数据分析库，使用它们，能够解决大部分的数据分析问题。

快速入门:

```py
import matplotlib.pyplot as plt # 一般需要用到的函数都在pylot当中
import numpy as np
# 设置自变量和因变量
x = np.linspace(-1, 1, 50)  # 从-1到1生成50个点
y = x**2
plt.plot(x, y)  # 绘制线条
plt.show()  # 展示图像
```

<img src="../../Pictures/数据分析/微信截图_20231030205534.png" align="left" style="zoom:40%;" />

> 其中，生成线图需要函数`.plot()`；显示图形需要函数`.show()`。

- `plot()`一般是用来绘制线条，最简洁的调用方式是直接传入一个数组对象y；使用时习惯将x和y都传入

- `show()`的功能是显示所有打开的图形

### 3.1设置基本信息

**创建图形**

`figure()`函数的功能就是为了创建一个图形figure，或者激活一个已经存在的图形figure，其原型如下:

```py
.figure(num=None, figsize=None, dpi=None, facecolor=None, edgecolor=None, frameon=True)
```

常用参数介绍:

- `num`: 传入一个整数或字符串，作为该figure独一无二的ID标识
- `figsize`: 传入一个二元组，分别表示该figure宽高
- `facecolor`: 设置背景色，默认白色
- `edgecolor`: 设置边框颜色

```py
x = np.linspace(-np.pi, np.pi, 256)
y1 = np.sin(x)
y2 = np.cos(x)
# 创建第一个figure对象
plt.figure(num='first')
plt.plot(x, y1)
 # 创建第二个figure对象
plt.figure(num='second')
# 该figure包含两个数学函数
plt.plot(x, y1)
plt.plot(x, y2)
plt.show()
```

<img src="../../Pictures/数据分析/图片1.png" align="left" style="zoom:10%;" />

> *注意，在创建第一个figure对象直至第二个figure对象出现前，绘制出的线条都属于该figure对象。*

**设置标题**

使用`title()`设置图像标题，其原型为:

```py
.title(label, fontdict=None, loc=None, pad=None, *, y=None, **kwargs)
```

常用参数介绍:

- `label`：设置标题文本
- `fontdict`：控制文本的字体属性，参数类型为字典，包含`fontsize`、`fontweight`、`color`、`verticalalignment`、`horizontalalignment`等等
- `loc`：设置标题位置，可选参数包括`left`, `center`, `right`，默认值为`center`
- `y`: 设置高度

```py
plt.title("Logarithmic function")
x = np.arange(0.000000001, 1, 0.001)
y = np.log10(x)
plt.plot(x, y)
plt.ylim((-2, 1))
plt.show()
```

<img src="../../Pictures/数据分析/微信截图_20231031140555.png" align="left" style="zoom:40%;" />

**绘制线条**

绘制线条使用`plot()`函数，其原型如下:

```py
.plot([x], y, [fmt], data=None, **kwargs)
```

最简洁的调用方式是直接传入一个数组对象y。可选参数`[fmt]`是一个字符串来定义图的基本属性如：颜色`color`，粗细`linewidth`，线型`linestyle`。

其中，`color`的可选参数有`blue`、`green`、`red`、`cyan`、`yellow`、`black`、`white`等常见颜色；

`linewidth`默认值是1.0；`linestyle`默认值是实线,`linestyle='--'`则代表虚线。

```py
x = np.linspace(-3, 3, 50)
y1 = 2 * x + 1
y2 = x**2
plt.figure()
plt.plot(x, y1)
plt.plot(x, y2, color="red", linewidth=1.0, linestyle="--") 
plt.show()
```

<img src="../../Pictures/数据分析/微信截图_20231030212845.png" align="left" style="zoom:40%;" />

**设置坐标信息**

- **限定取值范围**

一般地，我们可以通过设置`xlim`或者`ylim`来限制$x$轴和$y$轴的取值，参数传递一个包含最小值和最大值的二元组:

```py
.xlim((min_x,max_x))  # x取值范围
.ylim((min_y, max_y))  # y取值范围
```

这样设置后，$x$的取值会被限定在$min_x\leq x\leq max_x$，$y$的取值会被限定在$min_y\leq y\leq max_y$。

- **设置标签**

有时我们需要描述$x$，$y$轴的含义，使用`xlabel`或`ylabel`:

```py
.xlabel("x_axis")  # 描述x轴
.ylabel("y_axis")  # 描述y轴
```

> *注意，matplotlib 并不支持中文显示，如果标签存在中文字符串，可能会导致报错。如果确实需要使用中文，需要另外添加额外参数，这里不多赘述。*

综合上述代码，我们可以获得以下图像:

```py
plt.plot(x, y1)
plt.plot(x, y2, color="red", linewidth=1.0, linestyle="--")

plt.xlim((-1, 2))  # x取值范围
plt.ylim((-2, 3))  # y取值范围

plt.xlabel("x_axis")  # 描述x轴
plt.ylabel("y_axis")  # 描述y轴

plt.show()
```

<img src="../../Pictures/数据分析/微信截图_20231030213944.png" align="left" style="zoom:40%;" />

- **设置x轴刻度间隔**

如上图，目前$x$轴从-1到2之间间隔为7，我们可以通过`xticks`手动修改间隔，其原型为:

```py
.xticks(ticks=None, fontsize,fontweight,color,alpha,rotation,verticalalignment,horizontalalignment)
```

常用参数介绍:

- `ticks`: 可传递数组，x轴刻度位置的列表；传入空列表移除所有x轴刻度

- `fontsize`：设置标签的字体大小
- `fontweight`：设置标签的字体粗细，可选值为 `'normal'`、`'bold'`、`'light'`、`'ultrabold'`、`'heavy'`
- `color`：设置标签的颜色
- `alpha`：设置标签的透明度，取值范围为0到1
- `rotation`: 设置旋转度数
- `verticalalignment`：垂直对齐方式，可选值为 `'center'`、`'top'`、`'bottom'`、`'baseline'`
- `horizontalalignment`：水平对齐方式，可选值为 `'center'`、`'right'`、`'left'`

```py
# 调用linspace函数，包含5个元素
new_ticks = np.linspace(-1, 2, 5)
plt.xticks(new_ticks)
plt.show()
```

<img src="../../Pictures/数据分析/微信截图_20231030214434.png" align="left" style="zoom:40%;" />

修改后$x$轴的间隔变成5。

> 注意，如果$x$轴刻度过密，可能会导致坐标重叠，此时需要添加参数`rotaion`旋转角度即可，推荐`rotaion=-45`。

同理，如果需要调整$y$轴的间隔，使用`yticks()`即可。

- **设置y轴刻度为标签**

有时候我们希望y轴显示的并不是具体的数，而是数值的一个标签，可以调用`yticks`，并传入两个元素数量相等的列表作为对应:

```py
# 第一个列表是在y的取值范围中，需要变成标签的值，第二个列表就是对应的标签
plt.yticks([-2, -1.8, -1, 1.22, 3], ["common", "ok", "not bad", "good", "excellent"])
plt.show()
```

<img src="../../Pictures/数据分析/微信截图_20231030215454.png" align="left" style="zoom:40%;" />

### 3.2图像坐标化

在`Matplotlib`中与坐标轴相关的常用操作中，最终的成图还是留有瑕疵。图中的坐标轴看起来不那么舒服，原因在于不是日常所用的过原点$(0,0)$的坐标系，那么现在进行坐标轴位置优化。

> *注意，这一部分的代码记不住也没关系，因为这些都是标准化流程，不需要做出修改的，复制粘贴即可。*

在这整个过程里，我们需要使用`gca()`函数(*get current axis*)来实现对坐标轴的操作。

- 第一步，我们首先需要取消坐标轴上方和右侧的边框。

```py
ax = plt.gca()
# 将坐标轴的上方边框和右侧边框取消设置
ax.spines["right"].set_color("None")
ax.spines["top"].set_color("None")
plt.show()
```

<img src="../../Pictures/数据分析/微信截图_20231031081427.png" align="left" style="zoom:40%;" />

现在，只有两个坐标轴有黑色实线了，与数学的坐标系更为接近了。

- 第二，使$x$轴与$y$轴交汇于原点(0,0):

获取想要挪动的坐标轴，可选参数为顶部`top`、底部`bottom`、左`left`、右`right`四个方向参数。

```py
ax.xaxis.set_ticks_position('bottom')  #  要挪动底部的X轴，所以先目光锁定底部
# position位置参数有三种，这里用到了“按Y轴刻度位置挪动”
# 'data'表示按数值挪动，其后数字代表挪动到Y轴的刻度值
ax.spines['bottom'].set_position(('data',0))  # 使x轴交于y轴等于0的位置
```

同理设置$y$轴:

```py
ax.yaxis.set_ticks_position('left')
ax.spines['left'].set_position(('data',0))
plt.show()
```

<img src="../../Pictures/数据分析/微信截图_20231031082900.png" align="left" style="zoom:40%;" />

### 3.3图例和注解

有些时候需要添加一些图例来描述线条的简单信息，需要用到`legend()`函数。

- 在使用`plot`绘制线条时，添加参数`label`:

```py
# 使用'$'符号，采用Latex的语法:
plt.plot(x, y1, label="$2x+1$")
plt.plot(x, y2, color="red", linewidth=1.0, linestyle="--", label="$x^2$")
```

添加`legend()`显示图例:

```py
plt.legend()  # 不传参时，默认将图例放在数据量较少的位置显示
plt.show()
```

<img src="../../Pictures/数据分析/微信截图_20231031083941.png" align="left" style="zoom:40%;" />

如果我们需要精准的描述一个点或者输入较长的文本内容，还需要使用注解`annotate`或文本`text`。

#### 3.3.1设置注解

```py
.annotate(text,xy,xycoords,xytext,textcoords,color,weight,arrowprops)
```

常用参数介绍:

- `text`: 注解的文本内容

- `xy`: 注解的目标点坐标（$x_0, y_0$）
- `xycoords`: 目标点坐标的参考系，默认为"$data$"，表示使用数据坐标系

- `xytext`: 注解文本的偏移量（相对于目标点坐标），坐标系由*`textcoords`*确定

- `textcoords`: 注解文本坐标的参考系，默认为"offset points"，与$xy$值的偏移量
- `fontsize`: 注解文本的字体大小

- `weight`: 设置字体线型
- `color`: 设置字体颜色
- `arrowprops`: 用于绘制箭头的属性，比如箭头样式、连接样式等；参数类型为字典
- `bbox`: 给标题增加外框 

- **先优化坐标轴位置并绘制一条线**

```py
x = np.linspace(-3, 3, 50)
y = 2 * x + 1
plt.figure(num=1, figsize=(8, 5))
plt.plot(x, y)
ax = plt.gca()
ax.spines["right"].set_color("none")
ax.spines["top"].set_color("none")

ax.xaxis.set_ticks_position("bottom")
ax.spines["bottom"].set_position(("data", 0))
ax.yaxis.set_ticks_position("left")
ax.spines["left"].set_position(("data", 0))
```

- **再添加一个点(注解的对象)**

```py
x0 = 1
y0 = 2 * x0 + 1
# 借助散点图绘制一个点
plt.scatter(x0, y0, s=50, color="r")  # s代表size r代表red
plt.plot([x0, x0], [y0, 0], "k--", lw="2.5")  # k代表黑色black -- 代表使用虚线 lw代表linewidth
plt.show()
```

<img src="../../Pictures/数据分析/微信截图_20231031091607.png" align="left" style="zoom:40%;" />

- **添加注解**

```py
plt.annotate(
    # 文本使用Latex语法，使用'r'取消转义字符
    text=r"$while\,x=1,then\,y=3$",
    # 目标点和目标点的参考系
    xy=(x0, y0),
    xycoords="data",
    # 注解偏移量
    xytext=(+30, -30),
    textcoords="offset points",
    fontsize=16,
    # 设置箭头属性 箭头样式arrowstyle有'-'、'->'、'<-'、'<->'等等;连接样式connectionstyle有弧形连接arc3、直角连接angle、angle3等等
    arrowprops=dict(arrowstyle="->", connectionstyle="arc3,rad=.2")
)
plt.show()
```

<img src="../../Pictures/数据分析/微信截图_20231031091928.png" align="left" style="zoom:40%;" />

#### 3.3.2设置文本

```py
.text(x,y,string,fontsize,fontdict,verticalalignment,horizontalalignment,rotation,alpha,backgroundcolor,bbox)
```

常用参数介绍:

- `x,y`: 文本在坐标轴上的位置
- `string`: 设置文本内容
- `fontsize`: 设置字体大小
- `fontdict`:参数类型是字典，可以设置字体size、color等信息

- `horizontalalignment`: 设置水平对齐方式 ，可选参数包括`center` , `top` , `bottom` ,`baseline`

- `verticalalignment`: 设置垂直对齐方式，可选参数包括`left`,`right`,`center`
- `rotation`: 设置旋转角度，可选参数为`vertical`,`horizontal`也可以为数字
- `alpha`: 设置透明度，参数值0至1之间
- `backgroundcolor`: 设置标题背景颜色
- `bbox`: 给标题增加外框 



- **添加文本**

```py
plt.text(
    -3,
    3,
    r"$This\,is\,a\,text.\,\mu\,\sigma_i\quad\alpha_t$",
    fontdict={"size": 16, "color": "r"}
)  
plt.show()
```

<img src="../../Pictures/数据分析/微信截图_20231031095608.png" align="left" style="zoom:40%;" />

### 3.4绘制散点图

散点图使用`scatter()`函数，其原型如下:

```py
.scatter(x, y, s=None, c=None, marker=None, cmap=None, norm=None, vmin=None, vmax=None, alpha=None)
```

- `x，y`：长度相同的数组，也就是我们即将绘制散点图的数据点，输入数据

- `s`：点的大小，默认20，也可以是个数组，数组每个参数为对应点的大小

- `c`：点的颜色，默认蓝色`'b'`，也可以是个RGB或RGBA二维数组

- `marker`：点的样式，默认小圆圈`'o'`

- `norm`:，默认`None`，数据亮度在0~1之间，只有c是一个浮点数的数组的时才使用

- `vmin，vmax`：亮度设置，在`norm`参数存在时会忽略

- `alpha`：透明度设置，0-1 之间，默认`None`，即不透明

演示：

先随机出一组数据作为散点图的数据源:

```py
import numpy as np
n = 256
# 使用正态分布:分布的均值为0，标准差为1，生成n个数
X = np.random.normal(0, 1, n)
X
```

<img src="../../Pictures/数据分析/微信截图_20231031101744.png" align="left" style="zoom:40%;" />

```py
n = 256
# 设置X,Y的随机数
X = np.random.normal(0, 1, n)
Y = np.random.normal(0, 1, n)
# 设置颜色，知道即可
T = np.arctan2(Y, X) 
# 绘制散点图
plt.scatter(X, Y, s=75, c=T, alpha=0.5) 
# 限制x,y的取值
plt.xlim((-1.5, 1.5))
plt.ylim((-1.5, 1.5))
plt.show()
```

<img src="../../Pictures/数据分析/微信截图_20231031103025.png" align="left" style="zoom:40%;" />

如需隐藏$x,y$取值，只需补充`xticks()`或`yticks()`即可:

```py
plt.xticks(())  # 传递一个空元组，即不显示x轴取值
plt.yticks(())
plt.show()
```

<img src="../../Pictures/数据分析/微信截图_20231031103316.png" align="left" style="zoom:40%;" />

### 3.5绘制柱状图

柱状图原型如下:

```py
.bar(x, height, width=0.8, bottom=None,color,facecolor,edgecolor)
```

常用参数介绍:

- `x`: 为一个标量序列，确定x轴刻度数目
- `height`: 确定y轴的刻度
- `width`: 单个直方图的宽度，默认是0.8
- `bottom`: 设置y边界坐标轴起点，默认是0
- `color`: 设置直方图颜色（只给出一个值表示全部使用该颜色，若赋值颜色列表则会逐一染色，若给出颜色列表数目少于直方图数目则会循环利用）

- `facecolor`: 设置前景色
- `edgecolor`: 设置背景色

演示：

创建一个有序序列，并对应写出$y=f(x)$:

```py
n = 12
X = np.arange(n)
Y1 = (1 - X / float(n)) * np.random.uniform(0.5, 1.0, n)
Y2 = (1 - X / float(n)) * np.random.uniform(0.5, 1.0, n)
```

```py
# 使用16进制颜色代码表设置前景色
plt.bar(X, +Y1, facecolor="#9999ff", edgecolor="white")
plt.bar(X, -Y2, facecolor="#ff9999", edgecolor="white")
plt.show()
```

<img src="../../Pictures/数据分析/微信截图_20231031104546.png" align="left" style="zoom:40%;" />

- **设置并隐藏取值**

```py
plt.xlim(-0.5, n)
plt.xticks(())
plt.ylim(-1.25, 1.25)
plt.yticks(())
plt.show()
```

<img src="../../Pictures/数据分析/微信截图_20231031104725.png" align="left" style="zoom:40%;" />

- **添加数值信息**

添加信息依旧用到`text()`函数，由于每一个柱子都需要添加数值信息，所以需要通过循环来添加:

```py
# 将X和Y1打包成元组再遍历
for x, y in zip(X, Y1):
    # 设置文本所在的坐标位置，文本内容，水平和垂直对齐方式
    plt.text(
        x, y + 0.05, "%.2f" % y, ha="center", va="bottom"
    )  # ha: horizontal alignment va: vertical ...
# 同理遍历X,Y2
for x, y in zip(X, Y2):
    plt.text(x, -y - 0.05, "-%.2f" % y, ha="center", va="top")
    
plt.show()
```

<img src="../../Pictures/数据分析/微信截图_20231031111649.png" align="left" style="zoom:40%;" />



### 3.6绘制饼图

其原型如下:

```py
.pie(x, explode=None, labels=None, colors=None, pctdistance=0.6,autopct=None,shadow=False, labeldistance=1.1, startangle=None, radius=None, counterclock=True,textprops=None,wedgeprops=None)
```

常用参数说明：

- `x`：指定绘图的数据
- `explode`：指定饼图某些部分的突出显示，即呈现爆炸式
- `labels`：为饼图添加标签说明，类似于图例说明
- `colors`：指定饼图的填充色
- `autopct`：自动添加百分比显示，可以采用格式化的方法显示
- `pctdistance`：设置百分比标签与圆心的距离
- `shadow`：是否添加饼图的阴影效果
- `labeldistance`：设置各扇形标签（图例）与圆心的距离
- `startangle`：设置饼图的初始摆放角度
- `radius`：设置饼图的半径大小
- `counterclock`：是否让饼图按逆时针顺序呈现
- `textprops`：设置饼图中标签属性，如字体大小、颜色等
- `wedgeprops`: 设置饼图内外边界的属性

演示

```py
import matplotlib.pyplot as plt

x = [3423, 5601, 3759, 2400, 4050, 3145]  # 要展示的数据源
colors = ["#8DCCDD", "#9ACE9B", "#F2DF92", "#F4A8AA", "#EA8AAD", "#A094B2"]
plt.pie(
    x,
    colors=colors,  # 染色
    startangle=60,  # 设置初始角度为120°
    wedgeprops={"linewidth": 1.2, "edgecolor": "white"},  # 饼图内外边界的属性
    autopct="%.1f%%",  # 显示每个扇区的占比，保留1位小数，格式为%.1f%%
    pctdistance=0.6,  # 设置标签距离圆心的百分数为0.6
    textprops={"color": "white", "size": 11} # 添加文本标签属性
)
plt.show()
```

<img src="../../Pictures/数据分析/微信截图_20231104114952.png" align="left" style="zoom:40%;" />

## 4.实战演练

### 4.1柱状图

#### 4.1.1公司八月营业额

1. 绘制某公司8月份的营业额，假设这个月内总共营业了$X$天，且每日营业额为函数$Y=F(X)$，则:


```py
import matplotlib.pyplot as plt
import numpy as np
n = 20
X = np.arange(n)
# 假设Y与X的对应关系如下，表示在[-2,5)的区间内随机取n个整数
Y = np.random.randint(-2, 5, n) * X / 4 + 12
```

##### *渐变处理

为了提高直方图的观赏性，我们可以专门设置一下颜色的参数，这里使采用渐变色绘制，参考网站`https://photokit.com/colors/color-gradient/?lang=zh`

<img src="../../Pictures/数据分析/微信截图_20231031130625.png" style="zoom:70%;" />

可将这些颜色代码复制保存到列表中:

<img src="../../Pictures/数据分析/微信截图_20231031174525.png" align="left" style="zoom:40%;" />

- **绘制柱状图**:

```py
plt.bar(X, Y, color=color, edgecolor="white")
# 设置x轴标签
plt.xlabel(r"$The\,company's\,turnover\,in\, August$")
# y轴将原数据转换为对应的标签
plt.yticks([7,10,12],['deficit','balance','profit'])
# 限制x,y的取值范围
plt.xlim(0.5, 20)
plt.ylim(5, 30)
# 隐藏x轴
plt.xticks(())
plt.show()
```

<img src="../../Pictures/数据分析/微信截图_20231031130901.png" align="left" style="zoom:40%;" />

有时在我么们希望柱状图不仅仅展现出一个直方图，而是多个直方图，从而达到对比的目的。

#### 4.1.2地铁站人流量比对

2. 绘制出一张不同时间段内，3个不同车站的人流量对比柱状图。假设时间为$X$,3个车站所对应的人流量函数分别为$Y_1=W(X),Y_2=U(X),Y_3=V(X)$，则:

```py
import matplotlib.pyplot as plt
import numpy as np
# 设x轴的刻度为10
n = 10
X = np.arange(n)
# Y1,Y2,Y3与X的对应关系分别是
Y1 = np.random.randint(5, 20, n)
Y2 = np.random.randint(1, 25, n)
Y3 = np.random.randint(3, 30, n)
```

由于一个`bar`函数最后仅可传递一个$X$与$Y$，为了实现对比柱状图，我们需要创建3个不同的bar。在创建之前，为了直方图的美观度，可以先设置一下颜色。对于对比直方图，不建议用渐变色，因为对比度太低。我们可以选择一些搭配起来视觉效果较好的颜色，参考网站`https://zhuanlan.zhihu.com/p/96698715`。

- **绘制对比柱状图:**

##### *对比柱状图

```py
# 防止3个直方图重叠，可以将它们的x轴平移几个单位长度并修改它们的宽度
width = 0.8 / 3  # 由于直方图的默认宽度是0.8，而我们有3个直方图，所以修改宽度为0.8/3
plt.bar(X, Y1, width=width, label="Station 1", color="#E3A6A1")  # 添加图例以及颜色
plt.bar(X + width, Y2, width=width, label="Station 2", color="#BC5F6A")  # 平移x+width个单位
plt.bar(X + width * 2, Y3, width=width, label="Station 3", color="#19B3B1")
```

由于x轴实际代表时间，我们需要修改刻度值使其变成时间值:

```py
# 由于x轴的刻度为10，我们再补充刻度为10的时间值
time_range = []
for time in range(6, 25, 2):
    if time < 12 or time == 24:
        time_range.append(f"{time}.AM")
    else:
        time_range.append(f"{time}.PM")
plt.xticks(X + width, time_range, rotation=-15)  # 使其对齐中间的直方图，达到居中的效果；添加旋转度数，防止时间值重叠
plt.yticks(())  # 隐藏y轴刻度
```

最后，再补充标题:

```py
plt.title(
    "Comparison of passenger flow of three stations in different time periods",
    fontdict={"fontsize": 10}
)
# 显示图例
plt.legend()
# 显示图像
plt.show()
```

<img src="../../Pictures/数据分析/微信截图_20231031150403.png" align="left" style="zoom:40%;" />

#### 4.1.3文本长度分布

绘制一个柱状图，直观展现表格中某一列数据的文本长度统计:

- **数据预处理**

```py
import jieba as jb
import numpy as np
import pandas as pd
# 载入数据
df = pd.read_csv("待处理数据集.csv", encoding="ansi", sep=",")
df.shape  # 查看行和列数
```

```py
(36000, 7)
```

总共有36000条数据，由于难以将如此大的数据量都展示在一张图里，故我们只抽取其中的100行数据:

```py
random_index = np.random.randint(0, 36000 - 1, 100)  # 从这36000行数据中随机抽取100条，注意索引从0开始
random_index
```

<img src="../../Pictures/数据分析/微信截图_20231103094548.png" align="left" style="zoom:40%;" />

为了防止这里面出现重复的元素，可以使用`numpy`的`unique()`函数将数组中的重复元素去除:

```py
len(np.unique(random_index))
```

```py
100
```

去重后的数量依旧是100，说明这里面不存在重复的元素，那么这些就是我们需要做成柱状图的数据集对应的行索引:

```py
df = df.iloc[random_index, :]
df
```

<img src="../../Pictures/数据分析/微信截图_20231103095716.png" align="left" style="zoom:40%;" />

共得到了100行的数据，而我们所需要分析的文本长度就是名为"摘要"的这一列。但是由于它们都长文本，我们希望处理分析的对象是以字词为单位的数据结构，故我们在绘制图之前还需要对文本进行一定的预处理。

##### *文本分词和去停用词

`Jieba`是一个强大的Python中文分词库，主要功能是做中文分词，可以进行简单分词、并行分词、命令行分词。常用的分词函数有`cut()`和`lcut()`，其中，`.cut`生成的是一个generator，需要通过for循环来取里面的每一个词，通过print输出得到的是封装的数据；而`.lcut` 直接生成的就是一个list，通过print输出得到的是一个列表，故这里我们使用`lcut()`:	

```py
state_list = df["摘要"]  # 将我们需要处理的一列单独保存为一个列表
str_list = []  # 定义一个空列表，用于后续存储分词
for str in state_list:  # 遍历该列表得到每一个长文本
    str_list.append(jb.lcut(str))  # 将长文本进行分词，并储存到新列表
str_list
```

<img src="../../Pictures/数据分析/微信截图_20231103100801.png" align="left" style="zoom:40%;" />

> 另外，如果处理的数据集出现了比较陌生的词语，使得jieba将其错误地分开，可通过自定义分词的方式解决问题。自定义的词汇的方法： `jieba.load_userdict(file_name)` 参数是文本文件路径，txt、csv都可以。自定义词典文件的词汇格式是一个词占一行。

最终我们得到了一个这样的列表————该列表的每一个元素都是一个子列表，子列表下的每一个元素都是一个词语。

虽然此时我们已经得到了分词后的列表，但是这里不乏很多无效的词汇，如标点符号和无实际意义的词语，故还需要去停用词过滤文本。停用词库与分词库类似，一般储存在txt文件中，每一行代表一个停用词，可在网上下载到相关的中文停用词库:

```py
# 加载停用词库
stop_words = set()  # 使用集合方便去重
with open("停用词库.txt", encoding="utf8") as f:
    contents = f.readlines()  # 读取每行的数据并储存到列表中
    for word in contents:
        stop_words.add(word.strip())  # 去除每行的换行符后添加到集合中
stop_words
```

<img src="../../Pictures/数据分析/微信截图_20231103102302.png" align="left" style="zoom:40%;" />

现在对分词进行过滤，把过滤后的数据储存到新数据集中:

```py
data = []
for str in str_list:
    temp = []  # 定义一个临时列表，存储每一个子列表中过滤后的元素
    for word in str:  # 遍历得到每一个词语进行判断
        if word not in stop_words:
            temp.append(word)
    data.append(temp)
del temp
data
```

<img src="../../Pictures/数据分析/微信截图_20231103102709.png" align="left" style="zoom:40%;" />

- **统计分词后的文本数量**

为了方便后续绘制长度分布柱状图，现在要对该数据集每一个子列表中元素数量(所有分词数目)进行统计:

```py
count = []
for str in data:
    count.append(len(str))
print(count)
print(len(count))
```

<img src="../../Pictures/数据分析/微信截图_20231103103046.png" align="left" style="zoom:40%;" />

得到这100行数据每行摘要的有效文本长度。

- **绘制长度分布柱状图**

由于这次的数据共有100条，手动添加颜色的办法并不现实，所以这里采用了`colormaps()`函数获取颜色映射:

```py
import matplotlib.pyplot as plt

plt.figure(figsize=(9, 9))
"""
本次获取的是名为'rainbow'的颜色映射并使用linspace在0到1之间生成一个，长度为count
这个序列被用来在'rainbow'颜色映射中为count中的每个元素分配颜色
"""
cmap = plt.colormaps["rainbow"](np.linspace(0, 1, len(count)))  
plt.bar(
    np.linspace(1, 100, 100),
    count,
    width=0.3,
    color=cmap
)
plt.xticks(())
plt.ylim((40, 120))
plt.yticks(np.linspace(40, 120, 3))
plt.xlabel(r"$Length\ distirbution\ bar\ graph$",fontdict={'size':20})
plt.ylabel("$count$",fontdict={'size':20})
plt.show()
```

<img src="../../Pictures/数据分析/微信截图_20231103104907.png" align="left" style="zoom:40%;" />



### 4.2饼图

#### 4.2.1人气排行展示

绘制一个饼图，展示游戏某游戏人气排名前9的角色:

- **数据准备**

将保存到txt中的数据(每行数据均是"人名 票数"的格式)读取出来，分别存入两个列表作为饼图的`label`和`x`:

```py
with open("./《完蛋我被美女包围了》Top9.txt", encoding="UTF-8") as f:
    text = f.readlines()
names, scores = [], []
for line in text:
    line = line.strip()
    names.append(line.split(" ")[0])
    scores.append(int(line.split(" ")[1]))
```

为了增强饼图的视觉冲突，可以突出某些数据并填充适当的颜色:

```py
explode = [0.07, 0.02, 0, 0.04, 0, 0, 0.03, 0.1, 0.06]
colors = ["#63b2ee","#76da91","#f8cb7f","#f89588","#7cd6cf","#9192ab",
          "#7898e1","#efa666","#eddd86","#9987ce","#63b2ee","#76da91"]
```

- **绘制饼图**

```py
import matplotlib.pyplot as plt
# 由于这次的数据涉及到中文，需要设置一些参数以支持中文
plt.rcParams["font.sans-serif"] = ["SimHei"]  # 用来正常显示中文标签
plt.rcParams["axes.unicode_minus"] = False  # 用来正常显示负号
```

```py
plt.figure(figsize=(6, 6), facecolor="#e3ddbd")  # 创建figure并填充背景色
plt.title("《完蛋我被美女包围》人气Top9", y=1.25, fontdict={"size": 20})  # 设置标题
plt.pie(
    x=scores,
    labels=names,
    colors=colors,
    explode=explode,
    autopct="%.1f%%",  # 设置百分比的格式，这里保留一位小数
    startangle=180,  # 设置饼图的初始角度
    radius=1.5,
    counterclock=False,  # 是否逆时针，这里设置为顺时针方向
    shadow=True,
    pctdistance=0.5,  # 设置百分比标签与圆心的距离
    textprops={"fontsize": 19, "color": "white", "weight": "bold"}  # 设置标签属性，如字体大小为19，颜色为白色，粗体
)
plt.show()
```

<img src="../../Pictures/数据分析/微信截图_20231031175911.png" align="left" style="zoom:40%;" />

### 4.3词云图

绘制词云图需要导入`wordcloud`库，并由`matplotlib`展示。`WordCloud`原型如下:

```py
.WordCloud(background_color,max_words,width,height,layout,mask,max_font_size,color_func,colormap,font_path)
```

常用参数介绍:

`background_color`：词云背景的颜色，默认为白色

`max_words`：最多显示的词的数量，默认为所有可用词汇

`width` 、`height`：词云的宽度和高度，默认为自动调整以适应可用空间

`stopwords`：一个包含停用词的列表，停用词通常被认为是语言中的常见元素，但通常不需要在词云中出现；默认为空列表，表示使用所有可用词汇

`min_font_size`：最小的字体大小，小于此值的字体将被忽略，默认为1

`mask`：一个可选的遮罩图像，可以影响词云的布局和外观

`layout`：可选的布局选项，如`Jupyter`、`pack`或`generate`

`max_font_size`：最多使用的字体大小范围

`color_func`：用于根据文本内容或某些其他属性为词云中的词设置颜色

`colormap`: 设置颜色表

`font_path`: 设置自定义字体

实例化WordCloud对象后，还需要定义了要展示的文本字符串，该字符串格式为不同的词语之间使用空格分隔，最后使用`generate()`函数将文本传递给它。

#### 4.2.2文本分词词云

- **获取文本字符串**

根据之前处理文本分词的数据集，绘制出文本分词的词云图:

```py
from wordcloud import WordCloud as wc
temp=[]  # 定义一个临时列表，用于存储原先列表的所有分词
for words in data:
    for word in words:
        temp.append(word)
# 这样得到的列表元素就是分词，不存在嵌套的问题
temp
```

<img src="../../Pictures/数据分析/微信截图_20231103110819.png" align="left" style="zoom:40%;" />

定义文本字符串，包含了所有的分词，并以空格分隔:

```py
text=' '.join(temp)
del temp
text
```

<img src="../../Pictures/数据分析/微信截图_20231103111006.png" align="left" style="zoom:40%;" />

- **绘制词云图**

```py
plt.figure(figsize=(12, 12))
wordcloud = wc(font_path="HYZhengYuan-55W.ttf",background_color='white',colormap='viridis')  # colormap选择'viridis'
wordcloud.generate(text)
plt.xticks(())
plt.yticks(())
ax = plt.gca()
# 隐藏边框
ax.spines["top"].set_color("none")
ax.spines["bottom"].set_color("none")
ax.spines["left"].set_color("none")
ax.spines["right"].set_color("none")
# 通过imshow方法展示图像，interpolation参数用于控制图像的插值方式，使用'bilinear'插值使得词云中的每个词被渲染为更高质量的图像
plt.imshow(wordcloud, interpolation="bilinear")
```

<img src="../../Pictures/数据分析/微信截图_20231103111313.png" align="left" style="zoom:40%;" />
