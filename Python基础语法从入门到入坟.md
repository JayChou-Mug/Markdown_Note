# Python基础语法从入门到入坟

## 关于PyCharm

PyCharm是一种常用的Python IDE(集成开发环境)，带有一整套可以帮助用户在使用Python语言开发时提高其效率的工具，比如调试、语法高亮、Project管理、代码跳转、智能提示、自动完成、单元测试、版本控制。此外，该IDE提供了一些高级功能，以用于支持Django框架下的专业Web开发，界面编写代码和运行操作更加简单。

- **添加鼠标快捷键**

设置 - `setting` - `increase fonts size` - 右键 - `add mouse shortcut`，可以设置为ctrl + 鼠标滚轮向上

同理，搜索`decrease fonts size` ，设置为ctrl + 滚轮向下，最后点击右下角`apply`

此后可以通过快捷方式调整字体大小

- **添加中文汉化包和翻译软件**

设置 - `plugins` - 搜索"Chinese" - `install` - `apply `- 重启程序 - 完成

同样在插件中搜"`translation`"，按照以上方法操作即可

翻译使用时，先选中某个单词，右键 - `translation`，记得选择微软翻译，否则使用谷歌翻译由于网络原因加载不出来

- **常用快捷键**

> ctrl + `D` ：复制当前代码到下一行
>
> shift + alt + ↑/↓ ： 将当前代码上下移动
>
> ctrl + shift + `F10` ：运行当前代码
>
> shift + `F6` ： 重命名文件
>
> ctrl  + `F` ： 搜索
>
> ctrl + alt + `L` ：格式化代码
>
> ctrl + / ：快速添加/解除注释
>
> ctrl + `R` ： 快速（批量）替换
>
> ctrl + 左键 ：跟进源代码 

- **调试问题**

PyCharm自带的功能，检测Python文件中，以“test”开头的函数名，作为测试用例，导致在调试时，优先启动“test”函数，对于我们正常想调试的内容进行干扰。

如果不想使用这个功能，需要关闭，在设置 - `settings` - 搜索Python Integrated Tools - `Testing`，将选项修改为Unittests并应用即可。

------



## 1.关于Python程序

### 1.1程序构成

Python程序由模块组成，模块对应于扩展名为.py的源文件。一个Python程序由一个或者多个模块构成。模块由语句构成，模块即Python源文件。

### 1.2对象概述

在Python语言中，数据表示为对象。对象本质上是一个内存块，拥有特定的值，支持特定类型的运算操作。在Python3中，一切皆为对象，每个对象由标识**`(identity)`**、类型**`(type)`**和值**`(value)`**标识。

标识用于唯一识别一个对象，通常对应于对象在计算机内存中的位置。使用内置函数id可以返回对象的objl的标识：

```python
id(123)  # 140706558370656
```

类型和值会在后续中逐步介绍。

- **不可变对象和可变对象**

Python中的大部分对象都是不可变对象。例如`int`、`complex`等。对象本身值可以改变的对象称为可变对象(例如list、dict等)。变量是指向某个对象的引用，多个变量可以指向同一个对象。给变量重新赋值，并不改变原始对象的值，只是创建一个新对象，并将变量指向新对象。

### 1.3常量

Python语言不支持常量，没有语法规则限制改变一个常量的值。Python语言使用约定，声明在程序运行过程中不会改变的变量称为常量，通常使用全大写字母。

### 1.4命名规则

| 类型      |                                                              |
| --------- | ------------------------------------------------------------ |
| 模块/包名 | 全小写字母，简单有意义，如果需要可以使用下划线               |
| 函数名    | 全小写字母，可以使用下划线增加可读性                         |
| 变量名    | 全小写字母，可以使用下划线增加可读性                         |
| 类名      | 由多个单词组成名称，每个单词除了第一个字母大写外，其余字母均小写 |
| 常量名    | 全大写字母，可以使用下划线增加可读性                         |

### 1.5书写规则

1.使用换行符分隔，一般情况下一行一条语句。

2.从第一列开始，前面不能有任何空格，复合语句构造体必须缩进。

3.反斜杠`(\)`用于一个代码跨越多行的情况，如果语句太长，可以使用续行符`(\)`:

```python
print("如果语句太长，可以使用续行符,\
续行内容")
```

不过，三引号定义的字符串、元组、列表、字典可以放在多行，而不用使用续行符。

4.分号`(;)`用于在一行书写多条语句：

```python
a = 0 ; b = 0 ;c = 0;
```

### 1.6空语句

如果要表示一个空的代码块，可以使用pass语句：

```python
def do_nothing():
	pass
```



### 1.7输入输出语句

- **print()**

print()方法用于打印输出，是最常见的一个函数：

```python
print(*objects, sep=' ', end='\n', file=sys.stdout, flush=False)
```

> - `objects` -- 复数，表示可以一次输出多个对象。输出多个对象时，需要用 , 分隔。
>
> - `sep` -- 用来间隔多个对象，默认值是一个空格。
>
> - `end` -- 用来设定以什么结尾。默认值是换行符 \n，我们可以换成其他字符串。
>
> - `file` -- 要写入的文件对象。
>
> - `flush` -- 输出是否被缓存通常决定于 file，但如果 flush 关键字参数为 True，流会被强制刷新。

常用的有`end`参数，可以使得print语句不会默认换行处理：

```python
print("第一行")
print("第二行")
# 输出结果：
# 第一行
# 第二行
print('=' * 5)
print("第一行",end=' ')
print("还是第一行",end=' ')
# 输出结果：
# 第一行 还是第一行
```

另外，对于数据容器(列表、元组、字典、字符串等)而言，在变量名前输入一个`*`号，可以将数据容器中每一个元素取出来后再打印：

```python
list1 = [1, 2, 3]
print(list1)  # [1, 2, 3]
print(*list1)  # 1 2 3

s = "abc"
print(s)  # abc
print(*s)  # a b c
```

- **input()**

在执行键盘录入的时候，会使用input()语句：

```python
print("请输入你的年龄：")
age = input()
print(f"您的年龄是{age}岁")
```

为了简化代码，可以将在输入前的提示内容直接写到input()括号内：

```python
age = input("请输入你的年龄：")
```

*注意，input()语句不管录入的是什么数据，都会当作字符串处理。*

当需要一次录入多个数据时，可以使用下方语句：

```python
In [1]: a,b,c,d = input("请输入4个数字").split()
```

运行结果：

```python
请输入4个数字1 2 3 4

In [2]: a
Out[2]: '1'

In [3]: b
Out[3]: '2'

In [4]: c
Out[4]: '3'

In [5]: d
Out[5]: '4'
```

注意后方的`.split()`表示每一个字符串之间的分隔方式，默认为空。如果需要把分隔方式改成逗号，只需要在括号内传入','即可。

另外，如果需要把数据录入到一个列表里，可以使用一层for循环实现：

```python
namelist = list()
for _ in range(4):
    name = input()
    namelist.append(name)
namelist
```

运行结果：

```python
Aerith
Tifa
 Zack
 Cloud
['Aerith', 'Tifa', 'Zack', 'Cloud']
```

> 使用`input()`输入数据时，由于它的接受方式是字符串，所以只有换行才会终止输入。

------



## 2.关于数据类型

在Python当中，同样也有int、float、bool、string等数据类型，并且在创造变量的时候，会自动给数据分类，书写格式为

```python
name = "叶湘伦"  # 无需写String和分号
age = 19  # 无需写int
# 输出语句
print(name, "今年", age, "岁")
```

### 2.1整数类型

Python的整型对象**(int)**是不可变对象，整数位数可以为任意长度位数（只受限于计算机内存）。Python3.8支持使用下划线作为整数或者浮点数的千分位标记，以增强大数值的可阅读性。

整型通常解释为十进制数制，可以用前缀表示其他进制的整数，但在前缀后面的数字必须适合于数制：

| 数制               | 前缀   | 基本数码    |
| ------------------ | ------ | ----------- |
| 十进制(以10为基)   | \      | 0~9         |
| 十六进制(以16为基) | 0x(0X) | 0~9A~F[a~f] |
| 八进制(以8为基)    | 0o(0O) | 0~7         |
| 二进制(以2为基)    | 0b(0B) | 0~1         |



数字字符串(前面可以带负号"-")即整型字面量，Python解释器会自动创建int型对象实例：

```python
>>> a = 123
>>> type(a)  # <class 'int'>
>>> 1_000_000_000  # 1000000000
>>> 0x_FF_FF_FF_FF  # 4294967295
```

整数对象还支持关系运算、算术运算、位运算符、内置函数、math模块中的数学运算函数等运算操作。

### 2.2浮点类型

浮点类型**(float)**是表示实数的数据类型，与其他计算机语言的双精度(double)和单精度对应。Python浮点类型的精度与系统相关。浮点对象是不可变对象。

浮点型字面量可以为带小数点的数字字符串，或者使用科学计算法表示的数字字符串(前面可带负号)，即浮点型字面量，Python解释器自动创建float型对象实例。
$$
浮点型常量
$$

|          举例           |                        说明                         |
| :---------------------: | :-------------------------------------------------: |
|  1.23、-24.5、1.0、0.2  |                带小数点的数字字符串                 |
|         1.、.2          |                 小数点的前后0可省略                 |
| 3.14e-12、4E15，4.0e+15 | 科学计数法(e或E表示底数10)，例如3.14e-12=3.14*10^12 |

浮点数对象同样支持关系运算、算术运算、位运算符、内置函数、math模块中的数学运算函数等运算操作。

### 2.3复数类型

当数值字符串中包含虚数(j或J)时，即为复数**(complex)**字面量。complex是Python的内置数据类型，Python解释器自动创建其对象实例。

```python
complex(real,[,imag])  # 创建complex对象(虚部可选)
1 + 2j  # 输出(1 + 2j)
type(1 + 2j)  # 输出 <classs 'complex'>
c = complex(4,5)
c  # 输出(4 + 5j)
```

complex对象包含的属性和方法如下：
$$
complex对象包含的属性和方法
$$

|  属性/方法  |    说明    |               实例               |
| :---------: | :--------: | :------------------------------: |
|    real     | 复数的实部 |      >>> (1+2j).real  # 1.0      |
|    imag     | 复数的虚部 |      >>> (1+2j).imag  # 2.0      |
| conjugate() |  共轭复数  | >>> (1+2j).conjugate()  # (1-2j) |



### 2.4布尔类型

在Python中，布尔**(bool)**的真为Ture，假为False。在混合运算中，True自动转换为1，False自动转换为0。

布尔值字面量：

```python
print(type(True),type(False))  # <class 'bool'> <class 'bool'>
```

bool对象：

```python
print(bool(0))  # False
print(bool(1))  # True
print(bool('Python')) # True
```

有关布尔类型的混合运算：

```python
>>> 123 + True  # 124
>>> 123 + False  # 123
```



### 2.5检测数据类型

Python提供了检测变量数据类型的方法type()

```python
type1 = type("字符串")
print(type1) # <class 'str'>
print(type(type1))  # <class 'type'>
# 其自身类型就是type
```

*注意，在Python中变量是没有类型的，但它存储的数据是有类型的。*

### 2.6数据类型转换

Python提供了将一种数据类型转换为另一种数据类型的方法，方法名就是想要转换后数据类型的名称

```python
# 将数字转换成字符串
intStr = str(11)  # 将整型11变成字符串”11”
print(type(intStr), intStr)  # <class 'str'> 11

floatStr = str(3.14)
print(type(floatStr), floatStr)  # <class 'str'> 3.14

# 将字符串转换成数字
strInt = int("10")
print(type(strInt), strInt)  # <class 'int'> 10

strFloat = float("3.14")
print(type(strFloat), strFloat)  # <class 'float'> 3.14

# 其他情况
strBool1 = bool("")
print(type(strBool1), strBool1)  # <class 'bool'> False

strBool2 = bool("false")
print(type(strBool2), strBool2)  # <class 'bool'> True
```

*注意,字符串 "False" 在被转换为布尔值时，不会被解析为 False。任何非空的字符串都会被解析为 True。只有空字符串 "" 被解析为 False。*

------

## 3.关于类和对象

使用Python类可以定义自定义数据类型。类和对象是面向对象程序设计的两个主要方面，具体语法格式与Java类似。

**创建类对象**

Python使用复合语句class创建类对象：

```python
class 类名:
	类体
```

类体中可以定义属于类的属性、方法等。

**实例对象的创建和调用**

基于类对象可以创建其实例对象，然后访问其方法或属性。其语法格式如下：

```python
anObject = 类名(参数列表)
anObject.对象方法
anObject.对象属性
```

------



## 4.关于模块

Python模块**(Module)**就是一个Python文件，以.py结尾。模块能定义函数，类和变量，也能包括可执行的代码。

Python中有很多各种不同的模块，每一个模块都可以帮我们快速使用一些功能。可以认为一个模块就是一个工具包，每一个工具包中都有各种不同的工具供我们使用进而实现不同的功能。

### 4.1模块的语法

模块在使用前需要先导入，语法如下：

```python
[from 模块名] impoet [模块 | 类 | 变量 | 函数 | *] [as 别名]
常用的组合形式如下
import 模块名
from 模块名 import 类、变量、方法等
from 模块名 import *
import 模块名 as 别名
from 模块名 import 功能名 as 别名
```

现以Python自带的time模块为例

```python
# 使用import导入time模块

import time

# 通过.可以使用模块内部的所有功能（类、函数、变量）
time.sleep(5)

# 使用from导入时间模块中的sleep方法

from time import sleep
# 直接使用名字调用
sleep(5)

# 使用* 导入time模块的全部功能
from time import *
# 同样直接使用名字调用
sleep(5)

# 使用as给特定功能加上别名
# 当模块名或者模块功能名复杂时，可以将其改成简单的名字
import time as t
t.sleep(5)

from time import sleep as sl
sl(5)
```

### 4.2自定义模块

自定义的模块其实就是在创建一个.py文件，在另一个.py文件（同包）中使用它。

```python
# 创建一个名为my_module的.py文件
def test(a, b):
    print(a + b)
```

在另一个.py文件中

```python
# 导包1
import my_module1
# 调用方法（点调用）
my_module1.test(3, 7)
# 导包2
from my_module1 import test
# 调用方法（直接调用）
test(2,6)
# 导包 3
from my_module1 import *
# 调用方法（直接调用）
test(4, 5)
```

*注意，当导入多个模块后，如果调用到同名功能时，调用到的是后面导入的模块的功能。*

### 4.3main变量

如果模块当中包含了对自身函数的调用，在导入的时候也会先执行这一次调用。可以通过main变量取消该调用，语法如下

```python
自定义函数
if __name__ == '__main__':
    函数调用
#  这样只有当程序是直接执行的才会进入if内部,如果是被导入的，则if无法进入
```

在Pycharm中，直接输入main + 回车，Pycharm会自动帮我们补齐语句`if __name__ == '__main__':`

### 4.4all变量

如果一个模块文件中有all变量，当使用from xxx import * 导入时，只能导入这个列表中的元素。

```python
# 自定义模块
# all变量写在开头
__all__ = ['test_a']
def test_a(a, b):
    return a + b
def test_b(a, b):
    return a - b
```

在使用import *导包时，就只能调用到test_a，但其他导包方法不受all变量影响。

------

## 5.关于包

包其实可以理解成一个文件夹，在该文件夹下包含了一个`_init_.py`的文件。该文件夹可用于包含多个模块文件。所以其实包的本质依旧是模块。当我们的模块文件越来越多时，包可以帮助我们管理这些模块，包的作用就是包含多个模块。

以Pycharm为例，新建包（Python Package）后，包内部会自动创建`_init_.py`的文件，这个文件控制着包的导入行为。如果没有这个文件，那这个就属于一个普通文件夹。

接着在这个包下就可以创建多个模块，它们都属于这个包的范围。

### 5.1导包方式

```python
# 方式1
import 包名.模块名

调用方法
包名.模块名.函数名

# 方式2
from 包名 import 模块名

调用方法
模块名.函数名

# 方式3
from 包名.模块名 import 函数名

调用方法
函数名
```

*注意，必须在`_init_.py`文件中添加`__all__ = []`，控制允许导入的模块列表（针对使用from ... import 方式导入）。*

### 5.2安装第三方包

在Python程序的生态中，有许多第三方包(非Python官方)，可以极大的帮助我们提高开发效率，如:

> 科学计算中常用的: `numpy包`
> 数据分析中常用的: `pandas包`
> 大数据计算中常用的: `pyspark、apache-flink包`
> 图形可视化常用的:  `matplotlib、pyecharts包`
> 人工智能常用的:  `tensorflow包`

**安装方法**

`方法1：`

只要电脑中下载过Python，Python就有一个内置的pip(全称为Python Package Install)程序。打开cmd，输入pip install 包名 即可通过网络快速安装第三方包。

`方法2：`

由于方法1是直连外国的网址，网速受限，可以使用方法2安装。先ctrl + C 强制终止下载，然后将命令行指令修改成`pip install -i https://pypi.tuna.tsinghua.edu.cn/simple +包名`。

`方法3：`

打开Pycharm，找到解释器的按钮（显示Python版本号的地方），点击`Interpreter Settings`，在弹窗的列表中就会显示已经安装好的包，点击" + "号，在弹窗上方搜索包名，在列表中找到自己需要的，点击`Install Package`即可。

由于默认下载地址是Pycharm也是国外的网站，可以在右方勾选上`Options`按钮，输入`-i https://pypi.tuna.tsinghua.edu.cn/simple`连接指定网站下。

------



## 6.关于判断语句和选择结构

### 6.1关系和测试运算符

Python语言的关系和测试运算符如下：

| 运算符 | 表达式     | 含义                   |
| ------ | ---------- | ---------------------- |
| ==     | x == y     | x 等于 y               |
| !=     | x != y     | x 不等于y              |
| >      | x > y      | x 大于 y               |
| >=     | x >= y     | x 大于等于 y           |
| <      | x < y      | x 小于 y               |
| <=     | x <= y     | x 小于等于 y           |
| is     | x is y     | x 和 y 是同一个对象    |
| is not | x is not y | x 和 y 不是同一个对象  |
| in     | x in y     | x 是 y 的成员(y是容器) |
| not in | x not in y | x 不是 y 的成员        |

按优先级从高到低的顺序列出Python中的逻辑运算符：

| 运算符 | 含义   | 说明                                                  | 优先级 |
| ------ | ------ | ----------------------------------------------------- | ------ |
| not    | 逻辑非 | 当操作数为False时返回True；反之返回True               | 1      |
| and    | 逻辑与 | 两个操作数均为True时，结果才返回True，否则为False     | 2      |
| or     | 逻辑或 | 两个操作数中有一个为True时，结果即为True，否则为False | 3      |

### 6.2if语句

if 要判断的条件（不用加括号）:（冒号需要写）
    条件成立时，要做的事情
*注意，只要在if语句后有4个空格缩进的语句都会归属if判断的代码语句块执行，即Python通过缩进判断代码块的归属关系。*

```python
if 10 > 9:
    print(1)
    print(2)
print(3)
# 1 2 3
```

*注意，Python中可以使用if not语句表示取反。*

### 6.3if else语句

```python
age = 19
if age >= 18:
    print("您已成年")
else:
    print("您未成年")
# 注意else和if同级，不需要缩进
```

Python提供了下列条件表达式来实现等价于其他语言的三元条件运算符((条件)?语句1:语句2)的功能：

```python
条件为真时的值 if (条件表达式) else 条件为假时的值
```

例如，如果x$\geq$0，则y=x，否则y=0，可以表达为：

```python
x = int(input("x = "))
y = x if (x >= 0) else 0
print(f"y = {y}")
# 输入 1 y=1
# 输入 -1 y=0
```



### 6.4if elif else语句

elif即else if缩写

```python
if 判断1:
    代码1
elif 判断2:
    代码2
elif 判断3:
    代码3
    ......
else 判断n:
    代码n
```

### 6.5判断语句的嵌套

嵌套的关键点在于空格缩进，通过空格缩进，来决定语句之间的层次关系。

------



## 7.关于循环语句

### 7.1while循环

格式与C、Java类似：

> while 条件:
>     条件满足时，执行1
>     条件满足时，执行2
>     ...
>     条件满足时，执行n
> 循环结束时，执行n+1

```python
num = 1
while num < 9:
    print(num)
    num += 1
print("退出循环")
或者定义flag = True,
则while语句应为： while flag:
当条件满足时，flag = False
再次判断是时，由于flag为false，就会结束循环
```

或者定义flag = True，则while语句应为： while flag:
当条件满足时，flag = False；再次判断时，由于flag为false，就会结束循环

### 7.2for循环

格式如下：
for 临时变量 in 待处理数据集:

​	循环代码块

```python
word = "hello"
for x in word:
    print(x)
```

**else子句**

for，while语句可以附带一个else子句。如果for，while语句没有被break语句中止，则会执行else子句，否则不执行。其语法如下：

```python
for 变量 in 对象集合:
	循环体语句1
else:
	语句2
```

或者

```python
while 循环条件:
	循环体语句1
else:
	语句2
```

for可以遍历序列类型的数据，如字符串，列表，字典等等，其格式为:

```py
list = [1, 2, 3]
for elem in list:
    print(elem, end=' ')

print()
str = 'ABC'
for char in str:
    print(char, end=' ')

print()
dict = {1: 'first', 2: 'second', 3: "third"}
for key in dict.keys():
    print(dict[key], end=' ')

print()
```

其结果如下:

```py
1 2 3 
A B C 
first second third 
```

除了直接遍历这些数据容器外，还有一些常用的方法，如`enumerate`、`zip`:

通过枚举函数**`enumerate()`**遍历出索引和每一个字符。它返回一系列元组，元组第一个值为索引值，第二个元素为原对象。

```py
for idx,char in enumerate(str):
    print(idx,char)
```

```py
0 A
1 B
2 C
```

通过**`zip()`**函数用于将两个序列相对应位置的元素打包成元组。

```py
for elem, char in zip(list, str):
    print(elem, char)
```

```py
1 A
2 B
3 C
```

注意，当两个序列元素数量不对等时，循环的结束条件是遍历完元素数量较少的序列。

#### 7.2.1range语句

除了上述序列类型外，range语句可以获得一个简单的数字序列。它与C、Java中的`for(int i=0;i<n;i++)`的用法类似。

- **语法1：range(num)**

> 获得一个从0开始，到num结束的数字序列（不含num本身）
> 如range(5)取得的数据是[0,1,2,3,4]

- **语法2：range(num1, num2)**

> 获得一个从num1开始，到num2结束的数字序列（不含num2本身）
> 如range(5,10)取得的数据是[5,6,7,8,9]

- **语法3：range(num1, num2, step)**

> 获得一个从num1开始，到num2结束的数字序列（不含num2本身）
> 数字之间的步长，以step为准（默认为1）
> 如range(5,10，2)取得的数据是[5,7,9]

```python
for x in range(5):
    print(x)  # 0 1 2 3 4

for x in range(5, 10, 2):
    print(x) # 5 7 9
```

### 7.3continue与break

应对循环的临时跳过和直接跳出循环。使用方法与Java、C一致，不再赘述。当多个for、while语句彼此嵌套时，break语句只应用于最里层的语句，即break只能跳出最近的一层循环。

------



## 8.关于函数

### 8.1函数的定义

格式如下：

> def 函数名(传入参数):
>     函数体
>     return 返回值

```python
def add(a, b):
    return a + b


print("1+3=", add(1, 3))  # 4
```

*注意，Python当中的函数最后可以不写return，代表该函数无返回值，系统会自动返回None。而None有代表空，bool会将其判断为False，所以可以和bool配合使用。*

```python
def judge(x):
    if x >= 18:
        return True


flag = judge(12)
if not flag:  # 相当于非真即假
    print("您未成年")
else:
    print("您已成年")
```

### 8.2函数的文档说明

为了方便后期管理函数，可以在函数当中输入多行注释。当在函数当中输入好三引号并回车后，pycharm就会自动帮我们补充变量名。

```python
def state(x, y):
    """
    :param x:
    :param y:
    :return:
    """
    return x + y
```

### 8.3变量的作用域

#### 8.3.1全局变量

全局变量的作用域为其定义的模块，从定义的位置起，直到文件结束位置。不同的模块都可以访问全局变量。

#### 8.3.2局部变量

如果在一个函数中定义的局部变量(或形式参数变量)与全局变量重名，则局部变量优先。即函数中定义的变量是指局部变量，而不是全局变量。

```python
num = 100
def f():
	num = 200
	print(num)
f()  # 200
num  # 100
```

#### 8.3.3全局语句global

如果要为定义在函数外的全局变量赋值，可以使用global语句，表明变量时在外面定义的全局变量。global语句可以指定多个全局变量，如global x,y,z。

```python
pi = 3.14159265358979323846
def fun():
	global pi
    pi = 3.14
    print(f'global pi = {pi}')
print(f'before: pi = {pi}')  # before: pi = 3.14159265358979323846
fun()  # global pi = 3.14
print(f'now: pi = {pi}')  # now: pi = 3.14
```

#### 8.3.4非局部语句nonlocal

在函数体中可以定义嵌套函数，在嵌套函数中如果要为定义在上级函数体的局部变量赋值，可以使用nonlocal语句，表明变量不是所在块的局部变量，而是在上级函数体中定义的局部变量。同样，nonlocal可以指定多个非局部变量。

```python
def outer_fun():
    num = 10
    print(f'num={num}')
    def inner_fun():
        nonlocal num
        num = 5
        print(f'num={num}')
        # 调用函数
	inner_fun()
    print(f"num={num}")
outer_fun()
"""
num=10
num=5
num=5
"""
```

### 8.4函数的多返回值

和C、Java不同，Python当中函数可以返回多个结果。

```python
# 定义函数返回两个值，并使用两个变量接收
def fun():
    return 1, 2


a, b = fun()
print(f"a={a}, b={b}")  # a=1, b=2
```

> 注意，如果不使用变量接收或者只使用一个变量接收的话，得到的是一个元组：

```python
def fun():
    return 1, 2


print(fun())  # (1, 2)
a = fun()
print(f"a={a}")  # a=(1, 2)
```

当然，如果需要返回多个值，除了直接`return`多个值外，还可以返回一个元组或列表：

```python
# 生成由n个随机数构成的列表
import random


def randomarray(n):
    a = []
    for i in range(n):
        a.append(random.random())
    return a


b = randomarray(5)
print(f'type(b)= {type(b)}')
for i in b:
    print(i)
```

```python
type(b)= <class 'list'>
0.2391936427705107
0.03658923446117257
0.5708420899185046
0.7360116238431904
0.9628678721941636
```



### 8.5函数的多种传参方式

#### 8.5.1位置参数

调用函数时根据函数定义的参数位置来传递参数，传递的参数和定义的参数位置顺序和个数必须一致。

```python
def info(name, age, gender):
    print(f"姓名{name},年龄{age},性别{gender}")
info("叶湘伦", 19, "男")
```

#### 8.5.2关键字参数

函数调用时通过"键=值"形式传递参数。调用时，如果有位置参数，位置参数必须在关键字参数的前面，但关键字参数之间不存在先后顺序，且匹配参数顺序。

```python
info(name="叶湘伦", gender="男", age=19)  # 可以不按照固定顺序
```

#### 8.5.3缺省参数

缺省参数也叫默认参数，用于定义函数，为参数提供默认值，调用函数时可不传该参数的值、但所有位置参数必须出现在默认参数前，包括函数定义和调用。

```python
def info(name, age, gender="保密"):
    print(f"姓名{name},年龄{age},性别{gender}")

info("叶湘伦", 19)  # 姓名叶湘伦,年龄19,性别保密
info("叶湘伦", 19, "男")  # 姓名叶湘伦,年龄19,性别男
```

#### 8.5.4不定长参数

不定长参数也叫可变参数，通过带星`'*'`的参数，例如`*param1`，允许向函数传递可变数量的实参。调用函数时，从那一点以后的参数被收集为一个**元组**。

另外，也可以通过带双星号`**`的参数，允许向函数传递可变数量的实参。调用函数时，从那一点后的所有的参数被收集为一个字典。

> 注意，带星或者双星的参数必须位于**形参列表**的**最后位置**。

```python
# 利用带星和双星的参数计算各数字累加和
def sum(a, b, *c, **d):
    total = a + b
    for n in c:
        total += n
    for key in d:
        total += d[key]
    return total


print(sum(1, 2))  # 3
print(sum(1, 2, 3, 4, 5))  # 15
print(sum(1, 2, 3, 4, 5, male=6, female=7))  # 28
```



### 8.6函数作为参数传递

```python
def test_func(compute):
    result = compute(3, 2)
    print(f"computer的类型是{type(compute)}")
    print(f"计算结果是{result}")
```

不难看出，真正要计算的数据一定确定下来，唯一不确定的是计算的逻辑。所以，这是一种计算逻辑的传递，而非数据的传递。

```python
def compute1(x, y):
    return x ** y

def compute2(x, y):
    return y ** x
    
test_func(compute1)
# computer的类型是<class 'function'> 计算结果是9
test_func(compute2)
# computer的类型是<class 'function'> 计算结果是8
```

### 8.7lambda匿名函数

在函数定义中，def关键字，可以定义带有名称的函数。lambda关键字，可以定义匿名函数（无名称）。有名称的函数可以基于名称重复使用，而匿名函数只可临时使用一次。

```python
"""
定义语法
lambda 传入参数: 函数体(一行代码)
"""

# 修改上述代码
def test_func(compute):
    result = compute(2, 3)
    print(f"结果是{result}")

# 无需创建一个实体函数，而是在调用函数的同时写一个lambda函数
test_func(lambda x, y: x ** y)
```

### 8.8内置函数的使用

- **eval()**

使用内置的eval()函数可以对动态表达式进行求值：

```python
eval(expression, globals = None, locals = None)
```

其中，expression是动态表达式的字符串；globals和locals是求知时使用的上下文环境的全局变量和局部变量，如果不指定，则使用当前运行上下文。

```python
x = 3
str_func = input("请输入表达式:")
eval(str_func)  # 对表达式3 ** 2 + 3 * 2 + 1求职 输出: 16
```

eval()函数的功能是将字符串生成语句执行，如果字符串包含不安全的语句（例如删除文件的语句），则存在注入安全隐患。

- **exec()**

使用内置的exec()函数可以执行动态语句：

```python
exec(str[,globals[, locals]])
```

其中，str是动态语句的字符串。

```python
exec("for i in range(10):print(i,end='')")  # 输出： 0 1 2 3 4 5 6 7 8 9
```

通常，eval()函数用于动态表达式求值，返回一个值，exec()函数用于动态语句的执行，不返回值。

- **map()**

map()函数实现为内置的map(f,iterable,...)可迭代对象，将函数f应用于可迭代对象，返回结果为可迭代对象。简而言之，map()会根据提供的函数对指定序列做映射。

```python
list(map(abs,[-1,-3,-5,7,9]))  # [1,3,5,7,9]
```

自定义函数配合map函数：

```python
def add(x):
    return x + 1

list1 = [1,2,3,4,5]
out1 = list(map(add,list1))
print(out1)  # [2, 3, 4, 5, 6]
```

自定义函数的返回值一般为一个具体的数，并且一般使用list()去接收map()函数的返回值。

*注意：无论是map()函数还是filter()函数，提供给它们的函数不要带括号！*

- **filter()**

filter()函数实现为内置的filter(f,iterable)可迭代对象，将函数f应用于每个元素，然后根据返回值是True还是False决定保留还是丢弃该元素，返回结果为可迭代对象。

```python
def is_odd(x):
	return x % 2 == 1
list(filter(is_odd,range(10)))  # [1,3,5,7,9]
```

提供给filter()的函数返回值一般是布尔类型，只有返回True的时候，filter()函数才会记录这个数值，否则将其舍弃。

------



## 9.关于列表

### 9.1列表的定义

列表**（list）**的本质是一种有序的集合，元素可以重复，可以被修改，可以用下标索引查询，类似于Java，C当中的数组：

```python
# 定义变量
变量名 = [元素1, 元素2, ...]
# 定义空列表
变量名 = [];变量名 = list()
```



```python
list1 = ["叶湘伦", 19, "男"]
print(list1, type(list1))  # ['叶湘伦', 19, '男'] <class 'list'>
```

在Python当中，如果直接将列表名称输入到print中进行输出时，可以将其所有内容进行打印。

### 9.2列表的嵌套

列表支持嵌套

```python
list2 = [[1, 2], [3, 4]]
print(list2)  # [[1, 2], [3, 4]]
```

同时，可以根据其下标索引找到它对应的元素

```python
print(list1[0])  # 叶湘伦
print(list2[0][0])  # 1（类似于Java/C中取出二维数组值的方式）
```

> *注意，在Python中，从左到右的下标索引是0,1,2,....递增，从右到左的下标索引-1,-2,.....递减*

```python
print(list1[-1])  # 男
```

### 9.3列表的方法

#### 9.3.1查询元素索引

- **index()**

```python
print(list1.index(19))  # 1
```

> 注意，列表名[索引]得到的是该索引对应的元素值，而列表名.index(元素值)获得到的是对应的索引值

#### 9.3.2插入新元素

- **insert()**

```python
list1.insert(2, "大一")
print(list1)  # ['叶湘伦', 19, '大一', '男']
```

#### 9.3.3追加单个元素

- **append()**

```python
list1.append("理科")
print(list1)  # ['叶湘伦', 19, '大一', '男', '理科']
```

*注意以下区别：*

```python
list1 = [1, 2, 3]; list2 = [4, 5, 6]
list1.append(list2)  # [1, 2, 3, [4, 5, 6]]
print(list1)
list1 = [1, 2, 3]; list2 = [4, 5, 6]
list1.extend(list2)
print(list1)  # [1, 2, 3, 4, 5, 6]
```

#### 9.3.4追加多个元素

- **extend()**

```python
list1.extend(["数经", "数科"])
print(list1)  # ['叶湘伦', 19, '大一', '男', '理科', '数经', '数科']
```

如果使用extend()只传入单个元素(例如一个int)，就会发生报错：

```python
list1 = [1, 2, 3]
try:
    list1.extend(4)
    print(*list1)
except Exception as e:
    print(e)  # 'int' object is not iterable
```

这种情况下应该使用append()方法添加元素。

#### 9.3.5统计所有元素数量

- **len()**

```python
length = len(list1)
print(f"list1所有元素的数量有{length}个")  # list1所有元素的数量有9个
```

#### 9.3.6拷贝列表元素

```python
list1 = [1, 2, 3]
print(list1, id(list1))
list2 = list1.copy()
print(list2, id(list2))
```

```python
[1, 2, 3] 2359973367424
[1, 2, 3] 2359973370304
```

> 注意，使用该方法得到的新列表虽然列表元素值和原列表一致，但两者并不是同一个对象。

#### 9.3.7删除列表元素

删除列表元素共有以下4种方法

- **del**

```python
# 将6索引删除
del list1[6]
```

如果`del`的对象是列表本身，该方法可直接删除列表并释放其内存空间。

- **pop()**

该方法实际上是将指定元素从列表中提取出来，可以使用变量接收，再将该元素在列表中删除

```python
# 将6索引删除
element = list1.pop(5)
```

- **remove()**

如果该元素在列表中出现两次或以上，只会删除对应索引靠前的一个

```python
list1.remove("理科")
```

- **clear()**

```python
# 清除列表所有元素
list1.clear()
print(list1)  # []
```

#### 9.3.7统计元素出现数量

- **count()**

```python
list1 = [1, 3, 2, 3, 5, 8, 3, 12, 3]
print("3在list1中出现的数量为%d" % list1.count(3))  # 3在list1中出现的数量为4
```

#### 9.3.8列表的反转

```python
list1 = [1, 2, 3]
list1.reverse()
list1  # [3, 2, 1]
```



------



## 10.关于元组

相较于列表，元组**(tuple)**的特点是元素值不可以被篡改。元组一旦定义完成，就不可修改（封装数据）。

### 10.1元组的定义

```python
# 定义元组变量
变量名 = (元素1, 元素2, 元素3...)
# 定义空元组
变量名 = ();变量名 = tuple()
```

> 如果元组中只有一个元素时，后面的逗号不能省略，这是因为Python解释器会把(1)解释为1，把(1,)解释为元组

### 10.2元组的嵌套

```python
tuple1 = ((1, 2), (3, 4))
print(tuple1, type(tuple1))  # ((1, 2), (3, 4)) <class 'tuple'>
```

虽然元组的元素不可修改，但如果元组内嵌套了一个列表，那么列表内的元素仍可以修改。

```python
list3 = [19, "大一"]
tuple2 = ("叶湘伦", list3)  
print(tuple2)  # ('叶湘伦', [19, '大一'])
tuple2[1][0] = 20
tuple2[1][1] = "大二"
print(tuple2)  # ('叶湘伦', [20, '大二'])
```



### 10.3元组的方法

由于元组不可修改，所以相较于列表，方法会比较少

- 查找元素对应的索引**index()**



- 查看某元素出现次数**count()**



- 查看元组元素数量**len()**

------



## 11.关于字符串

Python中没有独立的字符数据类型(char)，字符即长度为1的字符串。Python内置数据类型str，用于字符串处理。str对象的值为字符序列，str对象是不可变对象。

### 11.1字符串的定义

字符串有三种定义法：

```python
str1 = '字符串1'  # 单引号定义
str2 = "字符串2"  # 双引号定义
str3 = """字符串3"""  # 三引号定义
```

其中三引号定义法和多行注释的写法一样，同样支持换行操作。当使用变量接受时，它就是字符串，否则当作多行注释使用：

```python
# 若想在字符串内包含引号，可以将字符串自带的引号前输入"\"转移字符取消它的作用
str4 = "\"字符串\""
print(str4)  # "字符串"
```

### 11.2字符串的运算

- **获取单个字符**

同元组一样，字符串也是有序、不可修改的数据容器，字符串中的每一个字符都会对应一个唯一的下标索引用来表示字符在字符串中的位置：

```python
str1 = "Hello World"
value1 = str1[1]
value2 = str1[-1]
print(value1, value2)  # e d
```

可以通过枚举函数**enumerate()**遍历出索引和每一个字符。枚举函数的基本语法如下：

```python
enumerate(可迭代对象，序号开始的值（默认为0）)
```

返回一系列元组，元组第一个值为索引值，第二个元素为原对象。

```python
str = "ABCDE"
for index, char in enumerate(str):
    print(f'index {index} = {char}')
```

输出结果如下：

```python
index 0 = A
index 1 = B
index 2 = C
index 3 = D
index 4 = E
```

> 其实，枚举函数可以适用于任何的数据容器，这里只是拿字符串举例。

- **获取部分字符(字符串切片)**

这部分内容请看第12章《关于切片》。

- **字符串相关运算**

Python中的字符串支持数学运算中的`+`和`*`，以及所有的比较运算符。

*`i)`*语法：字符串1 + 字符串2

说明：将字符串1和字符串2拼接在一起产生一个新的字符串。

> *注意：字符串不能和数字混合相加。也就是说`+`号只能拼接字符串，拼接其他类型数据则需要类型转换。*

```python
newstr = 'abc' + '123'
print(newstr)  # abc123
```

*`ii)`*语法：字符串*N

说明：N是正整数，实现N个字符串相加。

```python
newstr = 'abc' * 3
print(newstr)	# abcabcabc
```

*`iii)`*比较是否相等

说明：`==`， `!=`可以判断两个字符串是否相等或者不相等

> *注意：比较的直接就是两个字符串内容，并不是Java当中比较两个字符串对象的地址。*

```python
print('abc' == 'abc')	#True
print('abc' != 'abc')	#False
```

*`iv)`*比较大小

说明：从第一个字符开始依次往后找，到到第一个不相等的字符对，判断他们的编码值(Unicode)的大小，谁的编码值大，对应的字符串就大。

> *注意：当判断完首次出现编码值不同的字符后，立即返回真假值，不再往后比较下去。*

```python
print('b' > 'a')	#True
print('bc' > 'abc')	 #True
```

- **in和not in操作**

in判断字符串1是否在字符串2里面；not in判断字符串1是否不在字符串2里面：

```python
In [1]: 'abc' in 'hello abc'
Out[1]: True

In [2]: 'abc' in 'hello cba'
Out[2]: False

In [3]: 'abc' in 'hello cba'
Out[3]: False
```

### 11.2字符串的类型转换

将指定数据转换成指定类型，类型名是任何Python支持的，或者自定的类型都可以。对于字符串的类型转换，具体代码如下：

```python
>>> str1 = '100'
>>> type(str1)
<class 'str'>
>>> type(int(str1))
<class 'int'>

>>> str2 = '3.14'
>>> type(str2)
<class 'str'>
>>> type(float(str2))
<class 'float'>
```

### 11.3字符串的编码

Python3字符默认为16位Unicode编码，ASCII码是Unicode编码的子集。使用'u'或者'U'的字符串称之为Unicode字符串。Python3默认为Unicode字符串。使用内置函数ord(长度为1的字符串)(`unicode ordinal`，即编号)可以把字符转换为对应的Unicode码；使用内置函数chr(整型字面量)(`character`，即字符)可以把十进制数转换为对应的字符：

```python
>>> a = ord('A')
>>> a
65
>>> type(a)
<class 'int'>

>>> b = chr(65)
>>> b
'A'
>>> type(b)
<class 'str'>
```

注意，在C和Java中，都是使用ASCII编码，要区分Unicode和ASCII：

- **ASCII编码**

ASCII 码使用指定的7位或8位二进制数组合来表示128或256种可能的字符。由于ASCII是单字节编码，无法用来表示中文(中文编码至少需要2个字节)。

- **Unicode编码**

Unicode把所有语言都统一到一套编码里，这样就不会再有乱码问题了。Unicode最常用的是用两个字节表示一个字符(如果要用到非常偏僻的字符，就需要4个字节)。

**Unicode和ASCII的区别**

ASCII编码是1个字节，而Unicode编码通常是2个字节。

> 字母A用ASCII编码是十进制的65，二进制的01000001；而在Unicode中，只需要在前面补0，即为：00000000 01000001。

但是，如果文本里全部是英文的话，用Unicode编码比ASCII编码需要多一倍的存储空间，在存储和传输上就十分不划算。

### 11.4字符串的方法

同样的，字符串可以使用查找特定字符串的起始索引**index(字符串)**、统计字符串中某字符串出现的次数**count(字符串)**、统计字符串长度**len(字符串)**方法，以及：

#### 11.4.1字符串的替换

- **replace()**

```python
>>> str1 = "A Java Program."
>>> str1.replace("Java", "Python")
'A Python Program.'
```

该方法将字符串内的所有字符串1替换为字符串2，并得到一个新字符串

#### 11.4.2字符串的分割

- **split()**

在括号中输入分隔符字符串,结果就会将字符串划分为多个字符串并存入“列表对象”中：

```python
>>> str2 = "Hello World"
>>> list = str2.split(" ")
>>> list
['Hello', 'World']
```

#### 11.4.3字符串的分隔

- **join()**

该方法不会改变原有字符串，而是生成一个新的字符串。使用分隔符调用join方法，再传入需要分隔的字符串：

```python
>>> str1 = "12345"
>>> str2 = " | "
>>> str3 = str2.join(str1)
>>> str3
'1 | 2 | 3 | 4 | 5'
```

当join()括号内包含多个字符串时，不再对单个字符串的字符进行分隔，而是对字符串之间进行分隔：

```python
 # 对元组进行操作 
>>> seq = ('A','Python','Progarm')
>>> ' '.join(seq)
'A Python Progarm'
```

传入多个字符串时，可以得到一个新字符串将它们连接到一起：

```python
>>> str1 = "这是一段完整的话。"
>>> str2 = "这是第二段话。"
>>> str3 = ''.join.(str1, str2)  #长度为0的字符串调用join方法
这是一段完整的话。这是第二段话。
```

当需要把一个字符串列表`list`的所有元素拼接成一个大字符串时，可以使用下面语句：

```python
str2 = ''.join(str1 for str1 in list)
```



#### 11.4.4字符串规整操作

- **strip()**

从字符串中去掉在其左侧和右侧实参中列出的**字符**：

```python
# 不传参时，默认删除首尾空格和首位的转义字符
str1 = " Hello World "
print(f"修改前:{str1}")  # 修改前: Hello World 
print(f"修改后:{str1.strip()}")  # 修改后:Hello World

# 传参时，删除前后指定的字符串
str2 = "123412521"
print(f"修改前：{str2}")  # 修改前：123412521
str2 = str2.strip("12")
print(f"修改后：{str2}")  # 修改后：34125
# 实际上在底层会把传入的"12"当作字符'1'和字符'2'
str3 = "= python="
print(f"修改前：{str3}")  # 修改前：= python=
str3 = str3.strip(" =p")
print(f"修改后：{str3}")  # 修改后：ythp
```

#### 11.4.5字符串居中对齐

- **center()**

返回一个原字符串居中,并使用空格填充至长度width的新字符串。默认填充字符为空格

```python
str.center(width[, fillchar])
```

> *注意，格式中的[ ]内的参数都是可选参数，可以使用也可以不使用*

- `width`: 字符串的总宽度
- `fillchar`:  填充字符

```python
>>> str = 'runoob'
>>> str.center(20)  
'       runoob       '
>>> str.center(20, '*')  
'*******runoob*******'
```

#### 11.4.5字符串格式化

在11.2说过使用`+`号拼接字符串时，只能对字符串进行操作，无法拼接其他数据类型，但是我们可以通过借助占位符`%`可以解决字符串拼接时出现的问题：

```python
>>> str1 = "数字%d" % 123
>>> str1
'数字123'

>>> str2 = "数字%d和字母%s" % (150, "abc")   # 当出现多个变量占位，变量要用括号括起来，按占位的顺序填入
>>> str2
'数字150和字母abc'
```


占位符的对应关系是`%d -> int | %f -> float | %s -> string`。拼接符号从"+"变成"%"。

- **格式化的精度控制**

使用辅助符号"m.n"控制数据的宽度和精度。m控制宽度，如果设置的宽度小于数字自身则不生效；n控制小数点的精度，会进行小数的四舍五入。

> 例如`%5d`，即将整数的宽度控制在5位，如数字11被设置成5d，就会变成`[space][space][space]11`，用3个空格补足宽度。又如`%.2f`，即设置小数点精度为2。
> 如数字3.14159被设置`%.2f`后，结果是`3.14`（四舍五入）。

```python
float1 = 2.71828183
print("将自然常数e:", float1, "保留两位小数后是", "%.2f" % float1)  #将自然常数e: 2.71828183 保留两位小数后是 2.72
```

- **格式化的快速写法**

通过语法 f"内容{变量}"的格式来快速格式化。其中f代表format，该方式不关心类型也不关心精度控制，适合对精度没有要求的时候快速使用：

```python
>>> name = "叶湘伦"
>>> age = 19
>>> f"{name}今年{age}岁了"
'叶湘伦今年19岁了'
```

其实该方法是format()方法的简化使用，现在重点介绍format()方法。

##### 11.4.5.1format()方法

格式参数：

```python
'{[index][ : [fill] align][sign][#][width][.precision][type]}  {……}{……} '.format()
```

- `index`：指定冒号：后面出现的参数在‘format()’中的索引值，如果没有，则以format()中的**默认顺序**自动分配。
- `fill`：指定空白处的填充符。
- `align`:指定数字的对齐方式：

| align | 含义                                                         |
| :---: | ------------------------------------------------------------ |
|   <   | right-aligned 左对齐（对于大部分对象时为默认）               |
|   >   | right-aligned 右对齐 （对于数字时为默认）                    |
|   =   | 数据右对齐，同时将符号放置在填充内容的最左侧，该选项只对数字类型有效 |
|   ^   | 数据居中，此选项需和 width 参数一起使用                      |

- `sign`：指定有无符号数

- `width`：指定输出数据时所占的宽度
- `. precision`：如果后面存在type参数，则指的是保留小数的位数，如果type参数不存在，则是指有效数字的位数
- `type`：指定输出数据的具体类型

**format实例**

```python
# python ：^：代表居中显示数字567，位数width=10，fill=*（填充符为*）
>>> '{:*^10}'.format(567)  # '***567****'

# python :0是填充符，2是width，表示位数为2
>>> '{:02}:{:02}:{:02}'.format(13,4,57)  # '13:04:57'
```

**通过位置填充字符串**

```python
>>> 'hello {0} i am {1}'.format('world','python')  # 'hello world i am python'

>>> 'hello {} i am {}'.format('world','python')  # 'hello world i am python'

>>> 'hello {0} i am {1} . a now language-- {1}'.format('world','python')  #'hello world i am python . a now language-- python'
```

**通过key填充**

```python
obj = 'world'
name = 'python'
print('hello, {obj} ,i am {name}'.format(obj = obj,name = name))  # hello, world ,i am python
```

**通过列表填充**

```python
list=['world','python']
print('hello {names[0]}  i am {names[1]}'.format(names = list)  # hello world  i am python
print('hello {0[0]}  i am {0[1]}'.format(list))  # hello world  i am python
```

**通过字典填充**

```python
dict={'obj':'world','name':'python'} 
print('hello {names[obj]} i am {names[name]}'.format(names = dict))  # hello world i am python 
```



------

## 12.关于序列

序列数据类型是Python基础的数据结构，是一组有顺序的元素的几个。序列数据可以包含一个或者多个元素(即对象，元素也可以是其他序列数据)，也可以是一个没有任何元素的空序列。Python内置的序列数据类型包括元组、列表、字符串和字节数据。

### 12.1序列的方法

- 序列的长度、最大值、最小值、求和

通过内置函数**len()**、**max()**、**min()**方法实现。内置函数**sum()**可以获取列表或者元组中各元素之和；如果有非数字元素，则导致TypeError；对于字符串和字节数据，也将导致TypeError。

```python
In [1]: t1 = [1,2,3,4]

In [2]: sum(t1)
Out[2]: 10

In [3]: t2 = (1,'a',2)

In [4]: sum(t2)
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
Cell In[4], line 1
----> 1 sum(t2)

TypeError: unsupported operand type(s) for +: 'int' and 'str'
```

### 12.2序列的索引访问

序列表示可通过索引下标访问的可迭代对象。例如，用户可通过整数下标访问序列s的元素：`s[i]`。

索引下标从0开始，第1个元素为`s[0]`，以此类推，最后一个元素为`s[len(s)-1]`。索引下标也可从最后一个元素开始，即从-1开始，即最后一个元素为`s[-1]`，第1个元素为`s[-len(s)]`。

> 如果索引下标越界，则导致`IndexError`；如果索引下标不是整数，则导致`TypeError`。

```python
In [1]: s = 'abcdef'

In [2]: s[0]
Out[2]: 'a'

In [3]: t = (3.14, 11.45, 5.20)

In [4]: t[1]
Out[4]: 11.45

In [5]: l = [1, 2, 3, 4]

In [6]: l[3]
Out[6]: 4
```

### 12.3序列的切片

切片是从一个序列中取出一个子序列，语法格式如下：

> 序列名[起始下标: 结束下标: 步长]（不包含结束下标本身，留空时除外）。
> 起始下标可以留空，视作从头开始。
> 结束下标也可留空，视作截取到结尾。
> 步长表示依次取元素的间隔，默认为1。
> 当步长为负数，反向取（起始下标和结束下标也要反向标记）。

```python
>>> list1 = [0, 1, 2, 3, 4, 5, 6]
>>> list2 = list1[0:3]
>>> list2
[0, 1, 2]

>>> list3 = list1[:5:2]
>>> list3
[0, 2, 4]

>>> list4 = list1[::-1]  # 等同将序列反转
>>> list4
[6, 5, 4, 3, 2, 1, 0]

>>> str1 = "Hello World"
>>> str2 = str1[:str1.index(" ")]  # 截止到空格符的索引
>>> str2
'Hello'
```

实际案例1:

```python
# 将"切片练习"提取出来
>>> str1 = "odih习练片切sdoish"
>>> str1[4:8][::-1]
'切片练习'
```

实际案例2：

```python
# 获取星期字符
str = "一二三四五六日"
pos = input("请输入星期数字(1-7):")
try:  # 关于异常的知识请看17章
    num = int(pos)
    str = f"星期{str[num - 1:num]}"
    print(f"{num}对应的是{str}")
except ValueError as e:
    print("请输入正确的数字!")
"""
请输入星期数字(1-7):4
4对应的是星期四    
"""
```

### 12.4all()和any()

通过内置函数`all()`和`any()`可以判断序列的元素是否全部和部分是True。

- all(iterable) ： 如果序列的所有值都为True，返回True；否则返回False

- any(iterable) ： 如果序列的任意值为True，返回True；否则返回False

  ```python
  In [1]: list = [1, 2, 0]
  
  In [2]: any(list)
  Out[2]: True
  
  In [3]: all(list)
  Out[3]: False
  ```

  

------



## 13.关于集合

集合**(set)**自带去重功能，内部无序(不支持索引访问)，但允许修改。

### 13.1集合的定义

```python
变量名 = {元素1, 元素2, ...}
# 定义空集合
变量名 = set()

set1 = {"叶湘伦", 19, "大一", "叶湘伦", 19, "大一"}
print(set1)  # {'大一', '叶湘伦', 19}
```

### 13.2集合的方法

除了常规的清空集合clear()、统计集合元素数量len()以外，常用的还有：

#### 13.2.1添加新元素

- **add()**

*只有不是重复元素才会被真正添加到集合，注意和列表添加新元素append()方法进行区分*

```python
set1.add("理科")
print(set1)  # {'大一', '叶湘伦', 19, '理科'}
```

#### 13.2.2移除元素

- **remove()**

由于没有索引，所以移除元素时只能将该元素作为参数传递

```python
set1.remove("大一")
print(set1)  # {'叶湘伦', 19, '理科'}
```

#### 13.2.3随机取出元素

- **pop()**

```python
element = set1.pop()
print(element, set1)  # 叶湘伦 {19, '理科'}
```

*注意，取出元素后，该元素会从集合中被删除。*

#### 13.2.4两个集合的差集

- **difference()**

取出set1有而set2没有的元素组成一个新集合：

```python
set1 = {1, 2, 3, 4}
set2 = {1, 3, 6, 11}
set3 = set1.difference(set2)  
print(set3)  # {2, 4}
```

- **difference_update()**

取出set1有而set2没有的元素，并最终改变set1的元素：

```python
set1 = {1, 2, 3, 4}
set2 = {1, 3, 6, 11}
set1.difference_update(set2)
print(set1)  # 2 4
```

#### 13.2.5两个集合的并集

- **union()**

将set1和set2的元素进行合并，并剔除重复元素，组成一个新集合

```python
set1 = {1, 2, 3, 4}
set2 = {1, 3, 6, 11}
set3 = set1.union(set2) 
print(set3)  # {1, 2, 3, 4, 6, 11}
```

注意，该方法没有对应的`.._update()`方法直接改变set1。

#### 13.2.6两个集合的交集

- **intersection()**

```python
set1 = {1, 2, 3, 4, 5}
set2 = {3, 5, 11, 43}
set3 = set1.intersection(set2)
print(set3)  # {3, 5}
```

- **intersection_update()**

直接改变set1为两个集合的交集：

```python
set1.intersection_update(set2)
print(set1)  # {3, 5}
```

> 实际上，上述的交运算intersection()、并运算union()和差运算difference()都有相应的符号用来简化代码，分别是`'&、 | 、 -'`。
>
> 代码如下：
>
> ```python
> >>> set1 = {1, 2, 3, 4, 5}
> >>> set2 = {3, 5, 11, 43}
> >>> set3 = set1 & set2  # 等效于intersection(set2)
> >>> set4 = set1 | set2  # 等效于set1.union(set2)
> >>> set5 = set1 - set2  # 等效于set1.difference(set2)
> >>> set3
> {3, 5}
> >>> set4
> {1, 2, 3, 4, 5, 43, 11}
> >>> set5
> {1, 2, 4}
> ```
>
> > 另外，该方法也可以用于处理列表。但首先需要将列表转换成集合(剔除相同元素)再进行相应操作：
> >
> > ```python
> > list1 = [1, 2, 4, 6, 5, 20, 2, 1]
> > list2 = [3, 6, 23, 4, 8, 4]
> > set1 = set(list1) & set(list2)
> > print(set1)  # {4, 6}
> > ```

### 13.3集合的遍历

由于集合不支持下标索引，无法使用while循环遍历，但可以使用for循环

```python
for x in set1:
    print(x)  # 1 2 3 4
```



------



## 14.关于字典

### 14.1hash值

字典是键和值的映射关系。字典的键必须是可hash对象，即实现了`__hash__()`的对象。对象的hash值也可以使用内置函数hash()获取。

```python
In [1]: hash(100)
Out[1]: 100

In [2]: hash(1.23)
Out[2]: 530343892119149569

In [3]: hash('abc')
Out[3]: 4482109854951092690
```

不可变对象(bool、int、float、complex、str、tuple、frozenset等)是可hash对象，而可变对象通常是不可hash对象，因为可变对象的内容可以改变，因而无法通过hash()函数获得其hash值。字典的键只能使用不可变的对象，但字典的值可以使用不可变对象或可变对象。

### 14.2字典的定义

字典**(dict)**本质上是通过key找到value。字典同样使用{}表示，不过储存的元素是一个个的: 键值对
其中，字典不允许key重复，也不可使用索引。

```python
# 定义字典变量
my_dict = {key1:value1, key2:value2,....}
# 定义空字典
my_dict = {}
my_dict = dict()
```

> *注意，空字典才能用“{ }”表示，而集合不能。*

通过属性获取字典属性值的方式和数组类似，不过属性从下标索引改成了key。

```python
#  定义一个名字-分数对应的字典
In [1]: dict1 = {"Cloud": 60, "Aerith": 77, "Tifa": 98}

In [2]: dict1['Tifa']
Out[2]: 98
```

### 14.3字典的访问操作

- d[key]: 返回值为key的value；key不存在时会导致KeyError

- d[key]=value： 设置d[key]的值为value；如果key不存在，则新增键值对

- del d[key]： 删除字典元素；key不存在时会导致KeyError

- d.keys(): 返回字典d的键keys的列表

- d.values(): 返回字典d的值value的列表

- d.items(): 返回字典d的(key,value)对的列表

```python
dict = {"name": "叶湘伦", "age": "18", "gender": "男"}
print(f"keys = {list(dict.keys())}")
print(f"values = {list(dict.values())}")
print(f"items = {list(dict.items())}")
```

```python
keys = ['name', 'age', 'gender']
values = ['叶湘伦', '18', '男']
items = [('name', '叶湘伦'), ('age', '18'), ('gender', '男')]
```



### 14.4字典的方法

除了常规的删除元素pop() [将key作为参数传入，返回它所对应的value，并在字典中删除该键值对]、清空元素clear()、统计字典的元素数量len()以外，还有：

#### 14.4.1浅拷贝字典

```python
dict1 = {"name": "叶湘伦", "age": "18", "gender": "男"}
dict2 = dict1.copy()
dict2
```

```python
{'name': '叶湘伦', 'age': '18', 'gender': '男'}
```

#### 14.4.2获取指定key值

```python
dict.get(key[, value]) 
```

- key -- 字典中要查找的键。
- value -- 可选，如果指定键的值不存在时，返回该默认值。

```python
In [1]: dict =  {'Name': 'Runoob', 'Age': 27}

In [2]: dict.get('Age')  # 查找一个存在的key所对应的值
Out[2]: 27

In [3]: print(dict.get('Sex'))
None  # 没有设置 Sex，也没有设置默认的值，输出 None


In [4]: dict.get('Sex',0)  # 可以输出默认的值为0
Out[4]: 0
```

### 14.5字典的嵌套

> key支持字典以外的所有数据类型，value支持所有数据类型。

```python
# 将value作为一个字典对象
In [3]: dict2 = {
   ...: 	'Tifa' : {
   ...: 		'HP' : 80,
   ...: 		'MP' : 95,
   ...: 		'AP' : 67
   ...: 	}, 'Aerith' : {
   ...: 		'HP' : 86,
   ...: 		'MP' : 64,
   ...: 		'AP' : 84
   ...: 	}
   ...: }

In [4]: dict2
Out[4]:
{'Tifa': {'HP': 80, 'MP': 95, 'AP': 67},
 'Aerith': {'HP': 86, 'MP': 64, 'AP': 84}}

# 获取数据时，和二维数组类似，提供字典的两个key值
In [5]: dict2['Tifa']['MP']
Out[5]: 95
```

### 14.6字典的遍历

由于字典同样不支持索引，所以只能使用for循环遍历。

```python
# 方式1： 通过方法keys()获取到每一个key值作为序列
In [11]: for key in keys:
    ...:      print(f"name:{key}, score:{dict1[key]}")
    ...:
        
name:Cloud, score:60
name:Aerith, score:77
name:Tifa, score:98

# 方式2： 直接对字典进行for循环，系统内部自动帮我们调出其key值
In [12]: for key in dict1:
    ...:      print(f"name:{key}, score:{dict1[key]}")
    ...:
name:Cloud, score:60
name:Aerith, score:77
name:Tifa, score:98
```

------



## 15.关于数据容器

上述的列表、元组、字符串、集合和字典都属于数据容器。它们的通用操作都有：

### 15.1容器的遍历

遍历上，五类数据容器都支持for循环遍历。列表、元组、字符串支持while循环，集合、字典不支持。综上，它们都支持遍历操作。

### 15.2容器的方法

```python
# 数据容器都可以使用
len(容器) 统计元素个数
max(容器) 统计容器的最大元素
min(容器) 统计容器的最小元素
```

当字符与字符比较大小时，实际上是比较ASCII码表。字符串的比较实际上是按位比较，只要有一位大，就整体都大。

### 15.3容器的转换

容器的转换所用到的方法实际上就是转换后数据容器的名称。

```python
list(容器) 将给定容器转换为列表
str(容器)
tuple(容器)
set(容器)
```

### 15.4容器的排序

- **sorted()**

使用`sorted(容器,[reverse=True])`将给定容器进行排序，放入“列表”中。

```python
list1 = [3, 7, 9, 24, 36, 16, 75, 40]
print(sorted(list1))  # 正向排序（由小到大）
print(sorted(list1, reverse=True))  # 反向排序（由大到小）
```

> 有些时候，比如对于一个嵌套列表的列表，sorted()就无法帮我们实现自动排序，此时就需要我们使用另一个方法sort()来自定义排序。

- **sort()**

该方法的使用逻辑是被调用时，调用一个函数，该函数的作用提供排序规则，再将这个数据返回。格式为：

```python
列表.sort(key=排序规则, reverse=True/False)
```

案例分析

```python
# 准备列表
my_list = [["a", 33], ["b", 55], ["c", 11]]

# 排序，基于带名函数
def choose_sort_key(element):
    return element[1]

# 将元素传入choose_sort_key函数中，用来确定谁来排序，可以在最后一个参数输入reverse=True打开反转
my_list.sort(key=choose_sort_key, reverse=True)
print(my_list)  # [['b', 55], ['a', 33], ['c', 11]]
```

如果该函数只使用一次，还可以使用lambda匿名函数来简化代码，语法如下：

```python
sort(key=lambda 可迭代对象: 返回值 [,reverse=False])
```



```python
my_list = [["a", 33], ["b", 55], ["c", 11]]
# 排序，基于匿名函数
my_list.sort(key=lambda element: element[1], reverse=True)
print(my_list)  # [['b', 55], ['a', 33], ['c', 11]]
```

------



## 16.关于文件

### 16.1文件的读取

文件的打开需要用到open()函数

```python
f = open(name, mode, encoding)
```

> `name`: 要打开的目标文件名的字符串（可包含文件所在的具体路径）。
> `mode`:设置打开文件的模式（访问模式）：只读'r'、写入'w'、追加'a'，默认是只读方式。
> `encoding`:编码格式（推荐UTF-8）。

现在假设在C盘中有一测试.txt的文件，里面的内容如下：

> 你好Python
> 文件的读写
> 编码方式：UFT-8

现在可以使用Python对齐进行操作

```python
# 打开文件
f = open("C:/测试.txt", "r", encoding="UTF-8")
print(type(f))  # <class '_io.TextIOWrapper'>
```

*注意：书写路径时，需要用`"//"`或者`"\"`分隔，不允许使用单个`"/"`，因为它是转义字符。*

读取文件时有很多种方法，如

> 1.read(num) 
> num表示要从文件中读取的数据的长度（单位：字节），默认是读取文件中的所有数据，返回的是**字符串**
> 2.readlines()
> 按照行的方式把整个文件中的内容进行一次性读取，并且返回一个**列表**，列表中每一个元素代表文件的每行数据。
> 3.readline()
> 一次只读一行内容，返回的是**字符串**

```python
print(f"读取10个字节的结果是:{f.read(10)}")
# 读取10个字节的结果是:你好Python 文
print(f"读取全部内容的结果是:{f.read()}")
# 读取全部内容的结果是:件的读写
# 编码方式：UFT-8
lines = f.readlines()
print(f"lines对象的类型是{type(lines)}") 
# lines对象的类型是<class 'list'>
print(f"lines对象的内容是{lines}")  # lines对象的内容是[]
```

*注意，只要文件对象打开之后，后面无论调用什么方法，它都会续接上一次读取文件的位置进行读取。*

单独测试readline()方法

```python
line = f.readline()
print(line)  # 你好Python
```

for循环读取文件行

```python
count = 1
for line in f:  # 每一个临时变量line，负责记录文件的一行数据
    print(f"第{count}行的数据是{line}")
    count += 1
print("读取完毕")
"""
第1行的数据是你好Python

第2行的数据是文件的读写

第3行的数据是编码方式：UFT-8
读取完毕
"""
```

### 16.2文件的关闭

该方法关闭对文件的占用，如果不调用，同时程序没有停止，那么这个文件将一直被Python程序占用。

```python
f.close()
```

**with open语法**

通过在with open的语句块中对文件进行操作可以在操作完成后自动关闭文件，避免遗忘调用close()方法。

```python
with open("D:/测试.txt", "r", encoding="UTF-8") as f:
    f.readlines()
```

### 16.3文件的写出

写入文件使用write()方法。直接调用write后，内容并未真正写入文件，而是会积攒在程序的内存中，称为缓冲区。当调用flush时，内容会真正写入文件
这样做是避免频繁的操作硬盘，导致效率下降。

```python
f = open("D:/测试.txt", "w") # 模式w为写入模式
# 文件写入
f.write("Hello World")
# 内容刷新
f.flush()
# 关闭文件
f.close() # close方法内置了flush功能
```

*注意，文件不存在时，会自动创建文件并添加内容；存在时，则会将原内容清空再添加写入内容。*

### 16.4文件的追加

只需将模式从`'w'`改为`'a'`即可，其他方法与写出操作相同。如果需要换行写入，只需要添加"\n"即可。
文件不存在时，会自动创建文件并添加内容；存在时，直接在原内容后追加新添加的内容。

### 16.5os模块

使用标准库中的os模块***(operating system)***，用户可以实现操作系统的目录处理，例如创建目录、删除目录等操作。os模块主要包含`getcwd()`（获取当前工作目录）、`chdir()`（切换当前工作目录）、`mkdir()`（创建单级目录）、`makedirs()`（创建多级目录）、`listdir()`（显示目录中的文件/子目录列表）、`rmdir()`（删除目录）、`remove()`（删除文件）和`rename()`（文件或目录重命名）等函数。

**访问目录操作**

```python
In [1]: import os

In [2]: os.getcwd()  # 显示当前目录
Out[2]: 'C:\\Users\\Raymond'

In [3]: os.chdir('D:\\')  # 切换当前目录

In [4]: os.listdir(r'C:\Users\Raymond\Documents\Python')  # 列举当前目录中的内容
Out[4]:
['.idea',
 '.ipynb_checkpoints',
 '.virtual_documents',
 'B站爬取',
 'Numpy.ipynb',
 'Untitled.ipynb',
 '上机练习',
 '初识Python',
 '北京十年数据',
 '基于主题和词嵌入模型的专利文本自动分类',
 '小说爬取',
 '抢票脚本',
 '数据分析',
 '数据可视化',
 '数据采集',
 '数据预处理',
 '模拟用户登录',
 '爬取博客文章(URL管理器）',
 '第三方库学习',
 '豆瓣电影Top250']
```



#### 16.5.1返回当前目录的子目录

- **listdir()**

假设在D盘下有4个文本文件，分别叫A.txt、B.txt、C.txt、D.txt，则可以使用listdir()读取到这四个文件

```python
from os import listdir
directory = "D:"
for sub_path in listdir(directory):
    print(sub_print)
# A.txt B.txt C.txt D.txt
```

#### 16.5.2path模块

在os.path模块当中，有几个常用的方法，分别是：

```python
# 拼接路径
子目录完整路径 = join(上一级目录,文件夹名)  # <class 'str'> 功能相当于path=f"{directory}\\{sub_path_name}"
# 是否为文件
isfile()  # <class 'bool'>
# 是否为文件夹
isdir()  # <class 'bool'>
```

现在使用os模块中的功能实现取出入口文件夹的所有目录以及子目录：

```python
from os.path import join, isdir
from os import listdir


def get_dir(dir):
    for sub_path_name in listdir(dir):
        path = join(dir, sub_path_name)
        print(path)
        if isdir(path):
            get_dir(path)  # 如果是文件夹，使用递归


directory = "文件路径"
get_dir(directory)
```

如果不使用递归，可以通过while循环实现：

```python
from os import listdir
from os.path import join, isdir


def get_dir(dir):
    dirs = [dir]
    while dirs:  #循环结束的唯一条件是存放目录的列表中没有元素
        current_dir = dirs.pop(0)
        for sub_path in listdir(current_dir):
            path = join(current_dir, sub_path)
            print(path)
            if isdir(path):
                dirs.append(path)


directory = "文件路径"
get_dir(directory)
```

#### 16.5.3os中的常用方法

上述中已经提到了三种方法，分别是拼接完整路径、检查是否为文件或目录。其实，os.path还有很多方法：

| 方法                              | 说明                                                         |
| --------------------------------- | ------------------------------------------------------------ |
| abspath(path)                     | 返回绝对路径                                                 |
| basename(path)                    | 返回文件名                                                   |
| exists(path)                      | 如果路径path存在，返回`True`；如果路径path不存在或损坏，返回`False` |
| getsize(path)                     | 返回文件大小，如果文件不存在就返回错误                       |
| isabs(path)                       | 判断是否为绝对路径                                           |
| ***isfile(path)***                | ***判断路径是否为文件***                                     |
| ***isdir(path)***                 | ***判断路径是否为目录***                                     |
| ***join(path1[, path2[, ...]])*** | ***把目录和文件名合成一个路径***                             |
| realpath(path)                    | 返回path的真实路径                                           |
| samefile(path1, path2)            | 判断目录或文件是否相同                                       |



------



## 17.关于异常

### 17.1异常的类型

**1.语法错误**

**2.运行时错误**： Python程序的运行时错误是在解释执行过程中产生的错误。

**3.逻辑错误**： 程序可以执行(程序运行本身不报错)，但运行结果不正确。

常见的异常类型：

> - `NameError` 尝试访问一个未申明的变量。
>
> - `SyntaxError` 语法错误。
>
> - `AttributeError` 访问未知对象属性。
>
> - `TypeError` 类型错误。
>
> - `ValueError` 数值错误。
>
> - `ZeroDivisionError` 除零错误。
>
> - `IndexError` 索引超出范围。
>
> - `KeyError` 字典关键字不存在。

### 17.2异常的捕获

```python
# 基本语法
try:
   #  可能发生的异常
except:
   #  如果出现异常执行的代码
```

捕获指定异常

```python
try:
   #  可能发生的异常
except NameError as e:
    #  出现该异常时执行的代码
```

捕获所有异常

```python
try:
  #   可能发生的异常
except Exception（顶级异常） as e:
  #   出现异常时的解决方法
```

### 17.3else与finally

else表示如果没有异常时执行的代码，finally表示无论异常发生不发生都执行的代码，使用方法与Java一致。

综合案例

```python
str = input("请输入一个除数：")
try:
    num = int(str)
    print("3÷%d的结果是%d" % (num, 3/num))
except ValueError as e:
    print("除数不能为数字意外的字符！")
    print(e)  # 打印异常信息
except ZeroDivisionError as e:
    print("除数不能为0！")
    print(e)

except Exception as e:
    print("出现异常！")
    print(e)
else:
    print("计算完成！")
finally:
    print("运行结束！")
```

### 17.4异常的传递

和Java相似地，下层函数如果不及时处理异常，就会把异常向上抛给调用者。
当所有函数都没有捕获异常时，程序就会报错。只要函数有调用关系，可以在顶级的调用进行try catch语句捕获异常。但Python并不需要在函数头写“throws”。另外，在程序中，如果判断某种错误情况，则可以创建相应的异常类的对象，并通过**raise**语句抛出:

```python
if a < 0: raise ValueError("数值不能为负数！")
```

## 18.关于数值处理与计算

Python提供了丰富的数据类型和模块函数，用于程序设计中的数值处理和计算。

### 18.1math模块

$$
math\text{模块包含到的常用常量和函数API}
$$

| 名称            | 说明                       | 示例                   | 结果        |
| --------------- | -------------------------- | ---------------------- | ----------- |
| `e`             | 数学常量e                  | e                      | 2.71828…    |
| `pi`            | 数学常量pi                 | pi                     | 3.14159…    |
| `ceil(x)`       | 返回$\geq $x的最小整数     | ceil(1.2),ceil(-1.6)   | 2,-1        |
| `fabs(x)`       | 返回x的绝对值              | fabs(-1)               | 1           |
| `factorial(x)`  | 返回正整数x的阶乘          | factorial(3)           | 6           |
| `floor(x)`      | 返回$\leq $x的最大整数     | floor(1.8),floor(-2.1) | 1,-3        |
| `fmod(x,y)`     | 返回x % y                  | fmod(5,3)              | 2.0         |
| `trunc(x)`      | 将x截为最接近0的整数       | trunc(1.2),trunc(-2.8) | 1,-2        |
| `exp(x)`        | 返回$e^{\text{x}}$         | exp(5)                 | 148.413…    |
| `log(x[,base])` | 返回$In$x或者$log_{base}$x | log(e),log(e,2)        | 1.0,1.4426… |
| `log2(x)`       | 返回$log_2$x               | log2(e)                | 1.4426…     |
| `log10(x)`      | 返回$lg$x                  | log10(100)             | 2.0         |
| `pow(x,y)`      | 返回x$^{\text{y}}$         | pow(2,8)               | 256.0       |
| `sin(x)`        | 返回x的正弦                | sin(pi/2)              | 1.0         |
| `cos(x)`        | 返回x的余弦                | cos(2*pi)              | 1.0         |
| `tan(x)`        | 返回x的正切                | tan(pi/4)              | 0.999…      |

### 18.2random模块

random模块包含各种伪随机数生成函数，以及各种根据概率分布生成随机数的函数。该模块中大部分函数都基于random()函数，该函数使用`Mersenne Twister`生成器在[0.0,1.0]范围生成一致分布的随机值。

使用random模块函数`seed()`可以设置伪随机生成器的种子。基本形式如下：

```python
random.seed(a=None,version=2)
```

- a为种子，当没有指定a时使用系统时间。如果a为整数，则直接使用
- 当a不为整数且version=2时，a转换为整数。否则使用a的hash值

> 同一种子，每次运行产生的随机数相同(故称之为伪随机数)。

```python
In [1]: import random

In [2]: random.seed(1)

In [3]: for i in range(5): print(random.randint(1,5),end=',')
2,5,1,3,1,
In [4]: for i in range(5): print(random.randint(1,5),end=',')
4,4,4,4,2,
# 再次设置种子为1，结果重复
In [5]: random.seed(1)

In [6]: for i in range(5): print(random.randint(1,5),end=',')
2,5,1,3,1,

In [7]: random.seed(10)

In [8]: for i in range(5): print(random.randint(1,5),end=',')
5,1,4,4,5,
```

**常用随机函数**

| 名称                           | 说明                                              |
| ------------------------------ | ------------------------------------------------- |
| `random()`                     | 返回[0.0,1.0)之间的随机数                         |
| `randint(a,b)`                 | 返回随机整数N，使得a$\leq$N$\leq$b                |
| `randrange(start,stop[,step])` | 返回随机整数N，N属于序列[start,stop,step)         |
| `randrange(stop)`              | 返回随机整数N，N属于序列[0,stop)                  |
| `getrandbits(k)`               | 返回随机整数N，使得N的位(bit)长为k                |
| `uniform(a,b)`                 | 返回[a,b]之间的随机小数                           |
| `choice(seq)`                  | 从非空的序列seq中随机返回一个元素                 |
| `sample(pop,k)`                | 从非空的序列population随机抽取k个元素，返回其列表 |
| `shuffle(seq)`                 | 混排列表                                          |

### 18.3日期和时间处理

**相关术语**

- epoch

epoch(新纪元)是系统规定的的时间起始点。UNIX系统是1970/1/1 0:0:0开始。日期和时间在内部表示为从epoch开始的秒数。time模块中的函数对应C语言函数库中的函数，故只能处理1970/1/1到2038/1/1之间的日期和时间。

- UTC

UTC是协调世界时的英文缩写，是一种兼顾理论与应用的时标，旧称GMT(格林威治时间)。

- DST

DST即夏令时。不同地域可能规定不同的夏令时，C语言函数库使用表格对应这些规定。time模块中的daylight属性用于判定是否使用夏令时。

#### 18.31time模块

在系统内部，日期和时间表示为从epoch开始的秒数，称之为**时间戳**。time模块的struct_time对象是一个命名元组，用于表示时间对象，包括9个字段属性，即

`tm_year`年,`tm_mon`月,`tm_mday`日,`tm_hour`时,`tm_min`分,`tm_sec`秒,`tm_wday`星期,`tm_yday`一年中的第几天,`tm_isdst`是否夏令时。

time模块主要包含以下时间处理函数。

- time(): 获取当前时间戳。
- gmtime([secs]): 获取时间戳secs对应的**struct_time对象**，secs默认为当前时间戳。
- localtime([secs]): 获取时间戳secs对应的本地时间的struct_time对象，例如北京时间。
- ctime([secs]): 返回时间戳secs对应的本地时间字符串。
- mktime(t): localtime()的反函数，将本地时间struct_time对象t转换为时间戳。
- asctime([t]): 将时间元组或者struct_time对象t转换为时间字符串。
- sleep(secs): 暂停线程执行，让线程休息secs秒的时间。

示例

```python
In [1]: import time

In [2]: time.time()
Out[2]: 1698398642.0352635

In [3]: time.gmtime()
Out[3]: time.struct_time(tm_year=2022, tm_mon=10, tm_mday=27, tm_hour=9, tm_min=24, tm_sec=28, tm_wday=4, tm_yday=300, tm_isdst=0)

In [4]: time.localtime()
Out[4]: time.struct_time(tm_year=2022, tm_mon=10, tm_mday=27, tm_hour=17, tm_min=24, tm_sec=44, tm_wday=4, tm_yday=300, tm_isdst=0)

In [5]: time.ctime()
Out[5]: 'Fri Oct 27 17:24:53 2022'

In [6]: st = time.localtime()

In [7]: st.tm_year
Out[7]: 2022

In [8]: time.mktime(st)
Out[8]: 1698398715.0
```

**time模块程序运行时间测量**

time模块还包含了如下用于测量程序性能的函数。

- process_time(): 返回当前进程处理器运行时间。
- perf_counter(): 返回性能计数器。
- monotonic(): 返回单向时钟。

用户可以使用程序运行到某两处的时间差值，计算该程序片段所花费的运行时间，也可以使用time.time()函数，该函数返回以秒为单位的系统时间(浮点数)。

```python
import time


def fun():
    sum = 0
    for i in range(0, 10000000):
        sum += i
    return sum


t1 = time.monotonic()  # 单向时钟
print(fun())
t2 = time.monotonic()
print('运行时间:', t2 - t1)
"""
49999995000000
运行时间: 0.40600000000085856
"""
```

#### 18.32datetime模块

datetime模块包括datetime.MINYEAR和date.MAXYEAR两个常量，分别表示最小年份和最大年份，值为1和9999。

datetime模块包含用于表示日期的date对象、表示时间的time对象和表示日期时间的datetime对象。

> 通过datetime模块的datetime.today()函数可以返回表示当前日期的date对象，通过其实例对象方法，可以获取其年、月、日等信息。
>
> 通过datetime.now()函数可以返回表示当前日期时间的datetime对象。

示例

```python
import datetime

d = datetime.date.today()
dt = datetime.datetime.now()
print(f"当前日期是{d}")
print(f"当前日期和时间是{dt}")
print(f"ISO格式的日期和时间是{dt.isoformat()}")
print(f"当前年份是{dt.year}")
print(f"当前月份是{dt.month}")
print(f"当前日期是{dt.day}")
print(f"dd/mm/yyyy格式是{dt.day}/{dt.month}/{dt.year}")
print(f"当前小时是{dt.hour}")
print(f"当前分钟是{dt.minute}")
print(f"当前秒钟是{dt.second}")
```

```python
当前日期是2022-10-27
当前日期和时间是2022-10-27 17:48:25.816843
ISO格式的日期和时间是2022-10-27T17:48:25.816843
当前年份是2022
当前月份是10
当前日期是27
dd/mm/yyyy格式是27/10/2023
当前小时是17
当前分钟是48
当前秒钟是25
```

#### 18.33日期时间对象与字符串的转换

- **日期时间格式化为字符串**

time模块中的strftime()函数将struct_time对象格式化为字符串：

```python
time.strftime(format[,t])
```

其中，format为日期时间格式化字符串；可选参数t为struct_time对象。常用的日期时间格式化字符串如下表所示：

| 格式化字符串 | 日期/时间            |
| ------------ | -------------------- |
| **%Y**       | 年份0001~9999        |
| **%m**       | 月份01~12            |
| %B           | 月名January~December |
| %b           | 月名缩写Jan~Dec      |
| **%d**       | 日期01~31            |
| **%A**       | 星期Monday~Sunday    |
| %a           | 星期缩写Mon~Sun      |
| **%H**       | 小时(24h制)00~23     |
| %I           | 小时(12h制)01~12     |
| %p           | 上午/下午(AM/PM)     |
| **%M**       | 分钟00~59            |
| **%S**       | 秒00~59              |

示例

```python
In [1]: from time import *

In [2]: strftime("%c",localtime())
Out[2]: 'Sun Oct 29 11:25:47 2022'

In [3]: strftime("%Y年%m月%d日(%A)%H时%M分%S秒%p",localtime())
Out[3]: '2022年10月29日(Sunday)11时27分00秒AM'
```

同样，datetime.datetime.strftime()函数将datetime对象格式化为日期时间字符串：

```python
In [4]: import datetime

In [4]:  datetime.datetime.now().strftime('%Y - %m - %d %H: %M: %S')
Out[4]: '2022 - 10 - 29 11: 29: 28'
```

- **日期时间字符串解析为日期时间对象**

time模块中的strptime()函数将时间字符串解析为struct_time对象：

```python
time.strptime(string[,format])
```

> string为日期字符串；可选参数format为日期格式化字符串。

同样，datetime.datetime.strptime()将日期时间字符串解析为datetime对象：

```python
datetime.datetime.strptime(string,format)
```
