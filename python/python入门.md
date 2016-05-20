# Python study

> 参考：[Python入门简介](http://doc.oppoer.me/pages/viewpage.action?pageId=10027936)

### 第一个python程序
输出
``` python
print "hello world"
```
输入
```python
name=raw_input()
print name
```

### Python基础
##### **数据类型和变量**
> python 能够直接处理的数据类型：整数、浮点数、字符串、布尔值（True/False）、空值（None）
变量：必须是大小写英文、数字和_的组合，且不能用数字开头
常量：在Python中，通常用全部大写的变量名表示常量

##### **字符串和编码**
```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-
print 'Hi, %s, you have $%d.' % ('Michael', 1000000)
```
> 第一行注释是为了告诉Linux/OS X系统，这是一个Python可执行程序，Windows系统会忽略这个注释；
第二行注释是为了告诉Python解释器，按照UTF-8编码读取源代码，否则，你在源代码中写的中文输出可能会有乱码。

```python
print 'Hi, %s, you have $%d.' % ('Michael', 1000000)
```
> 格式化常见占位符：
%d  整数
%f  浮点数
%s  字符串
%x  十六进制整数


##### **使用list和tuple**
Python内置的一种数据类型是列表：list。list是一种有序的集合，可以随时添加和删除其中的元素。
```python
classmates = ['Michael', 'Bob', 'Tracy']
classmates.pop()
classmates.pop(1)
classmates.append(True)
print classmates
```
另一种有序列表叫元组：tuple。tuple和list非常类似，但是tuple一旦初始化就不能修改
```python
classmates = ('Michael', 'Bob', 'Tracy')
t = (1,)
```
> Python在显示只有1个元素的tuple时，也会加一个逗号,，以免你误解成数学计算意义上的括号。


##### **条件判断和循环**
条件判断
```python
age = 3
if age >= 18:
    print 'adult'
elif age >= 6:
    print 'teenager'
else:
    print 'kid'
```
循环
```python
names = ['Michael', 'Bob', 'Tracy']
for name in names:
    print name
```
> Python提供一个range()函数，可以生成一个整数序列

```python
sum = 0
for x in range(101):
    sum = sum + x
print sum
```

##### **使用dict和set**
Python内置了字典：dict的支持，dict全称dictionary，在其他语言中也称为map，使用键-值（key-value）存储，具有极快的查找速度。
```python
d = {'Michael': 95, 'Bob': 75, 'Tracy': 85}
print d['Michael']
```
> 和list比较，dict有以下几个特点：
查找和插入的速度极快，不会随着key的增加而增加；
需要占用大量的内存，内存浪费多。
而list相反：
查找和插入的时间随着元素的增加而增加；
占用空间小，浪费内存很少。
所以，dict是用空间来换取时间的一种方法。

set和dict类似，也是一组key的集合，但不存储value。由于key不能重复，所以，在set中，没有重复的key。
要创建一个set，需要提供一个list作为输入集合：
```python
s = set([1, 2, 3, 4])
s.remove(4)
```
两个set可以做数学意义上的交集、并集等操作
```python
s1 = set([1, 2, 3])
s2 = set([2, 3, 4])
print s1 & s2
print s1 | s2
```


### 函数
##### **调用函数**
```python
abs(-20)
cmp(1,10)
```
> python的官方网站查看文档http://docs.python.org/2/library/functions.html
在交互式命令行通过help(abs)查看abs函数的帮助信息

##### **定义函数**
定义函数
```python
def my_abs(x):
    if x >= 0:
        return x
    else:
        return -x
```
空函数
```python
def nop():
    pass
```
>  pass语句什么都不做，那有什么用？实际上pass可以用来作为占位符，比如现在还没想好怎么写函数的代码，就可以先放一个pass，让代码能运行起来。

参数检查
> 调用函数时，如果参数个数不对，Python解释器会自动检查出来，并抛出TypeError
如果参数类型不对，Python解释器就无法帮我们检查

```python
def my_abs(x):
    if not isinstance(x, (int, float)):
        raise TypeError('bad operand type')
    if x >= 0:
        return x
    else:
        return -x
```
> 添加了参数检查后，如果传入错误的参数类型，函数就可以抛出一个错误

返回多个值
```python
import math

def move(x, y, step, angle=0):
    nx = x + step * math.cos(angle)
    ny = y - step * math.sin(angle)
    return nx, ny

x, y = move(100, 100, 60, math.pi / 6)
print x, y
```
> 返回值是一个tuple！但是，在语法上，返回一个tuple可以省略括号，而多个变量可以同时接收一个tuple，按位置赋给对应的值，所以，Python的函数返回多值其实就是返回一个tuple，但写起来更方便。

> 定义函数时，需要确定函数名和参数个数；
如果有必要，可以先对参数的数据类型做检查；
函数体内部可以用return随时返回函数结果；
函数执行完毕也没有return语句时，自动return None。
函数可以同时返回多个值，但其实就是一个tuple。


##### **函数的参数**
默认参数
```python
def power(x, n=2):
    s = 1
    while n > 0:
        n = n - 1
        s = s * x
    return s

print power(5)
```
> 当我们调用power(5)时，相当于调用power(5, 2)：
当函数有多个参数时，把变化大的参数放前面，变化小的参数放后面。变化小的参数就可以作为默认参数。
使用默认参数有什么好处？最大的好处是能降低调用函数的难度。

可变参数
```python
def calc(*numbers):
    sum = 0
    for n in numbers:
        sum = sum + n * n
    return sum
print calc(1, 2)
print calc()
nums = [1, 2, 3]
print calc(nums[0], nums[1], nums[2])
print calc(*nums)
```
> Python允许你在list或tuple前面加一个*号，把list或tuple的元素变成可变参数传进去

关键字参数
> 可变参数允许你传入0个或任意个参数，这些可变参数在函数调用时自动组装为一个tuple。而关键字参数允许你传入0个或任意个含参数名的参数，这些关键字参数在函数内部自动组装为一个dict。

```python
def person(name, age, **kw):
    print 'name:', name, 'age:', age, 'other:', kw

person('Bob', 35, city='Beijing')
person('Adam', 45, gender='M', job='Engineer')
kw = {'city': 'Beijing', 'job': 'Engineer'}
person('Jack', 24, **kw)
```

参数组合
> 在Python中定义函数，可以用必选参数、默认参数、可变参数和关键字参数，这4种参数都可以一起使用，或者只用其中某些，但是请注意，参数定义的顺序必须是：必选参数、默认参数、可变参数和关键字参数。

```python
def func(a, b, c=0, *args, **kw):
    print 'a =', a, 'b =', b, 'c =', c, 'args =', args, 'kw =', kw


```

##### **递归函数**


