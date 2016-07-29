# Python study

> 参考：[Python入门简介](http://doc.oppoer.me/pages/viewpage.action?pageId=10027936)

----------

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

----------

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

----------

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
> 在函数内部，可以调用其他函数。如果一个函数在内部调用自身本身，这个函数就是递归函数。举例，计算阶乘n! = 1 x 2 x 3 x ... x n，用函数fact(n)


```python
def fact(n):
    if n==1:
        return 1
    return n * fact(n - 1)
```

> 递归函数的优点是定义简单，逻辑清晰。理论上，所有的递归函数都可以写成循环的方式，但循环的逻辑不如递归清晰。使用递归函数需要注意防止栈溢出。在计算机中，函数调用是通过栈（stack）这种数据结构实现的，每当进入一个函数调用，栈就会加一层栈帧，每当函数返回，栈就会减一层栈帧。由于栈的大小不是无限的，所以，递归调用的次数过多，会导致栈溢出。解决递归调用栈溢出的方法是通过尾递归优化，事实上尾递归和循环的效果是一样的，所以，把循环看成是一种特殊的尾递归函数也是可以的。

> 尾递归是指，在函数返回的时候，调用自身本身，并且，return语句不能包含表达式。这样，编译器或者解释器就可以把尾递归做优化，使递归本身无论调用多少次，都只占用一个栈帧，不会出现栈溢出的情况。

```python
def fact(n):
    return fact_iter(n, 1)

def fact_iter(num, product):
    if num == 1:
        return product
    return fact_iter(num - 1, num * product)
```

> 可以看到，return fact_iter(num - 1, num * product)仅返回递归函数本身，num - 1和num * product在函数调用前就会被计算，不影响函数调用。
尾递归调用时，如果做了优化，栈不会增长，因此，无论多少次调用也不会导致栈溢出。
遗憾的是，大多数编程语言没有针对尾递归做优化，Python解释器也没有做优化，所以，即使把上面的fact(n)函数改成尾递归方式，也会导致栈溢出。


> 使用递归函数的优点是逻辑简单清晰，缺点是过深的调用会导致栈溢出。
> 针对尾递归优化的语言可以通过尾递归防止栈溢出。尾递归事实上和循环是等价的，没有循环语句的编程语言只能通过尾递归实现循环。
> Python标准的解释器没有针对尾递归做优化，任何递归函数都存在栈溢出的问题。

----------

### 高级特性
##### **切片**

```python
L = range(100)
print L[0:3] # L[0:3]表示，从索引0开始取，直到索引3为止，但不包括索引3。即索引0，1，2，正好是3个元素。
print L[:3] # 如果第一个索引是0，还可以省略
print L[-10:] # 后10个数
print L[10:20] # 前11-20个数
print L[:10:2] # 前10个数，每两个取一个
print L[::5] # 所有数，每5个取一个
```
> tuple也是一种list，唯一区别是tuple不可变。因此，tuple也可以用切片操作，只是操作的结果仍是tuple
> 字符串'xxx'或Unicode字符串u'xxx'也可以看成是一种list，每个元素就是一个字符。因此，字符串也可以用切片操作，只是操作结果仍是字符串



##### **迭代**
> Python的for循环抽象程度要高于Java的for循环，因为Python的for循环不仅可以用在list或tuple上，还可以作用在其他可迭代对象上
```python
d = {'a': 1, 'b': 2, 'c': 3}
for key in d:
    print key
```
> 默认情况下，dict迭代的是key。如果要迭代value，可以用for value in d.itervalues()，如果要同时迭代key和value，可以用for k, v in d.iteritems()

> 如何判断一个对象是可迭代对象呢？方法是通过collections模块的Iterable类型判断
```python
from collections import Iterable
print isinstance('abc', Iterable)
print isinstance([1,2,3], Iterable)
print isinstance(123, Iterable) 
```

> Python内置的enumerate函数可以把一个list变成索引-元素对，这样就可以在for循环中同时迭代索引和元素本身
```python
for i, value in enumerate(['A', 'B', 'C']):
    print i, value
```


##### **列表生成式**
> 列表生成式即List Comprehensions，是Python内置的非常简单却强大的可以用来创建list的生成式
要生成list [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]可以用range(1, 11)：
要生成[1x1, 2x2, 3x3, ..., 10x10],可以[x * x for x in range(1, 11)]
写列表生成式时，把要生成的元素x * x放到前面，后面跟for循环，就可以把list创建出来，十分有用，多写几次，很快就可以熟悉这种语法。
for循环后面还可以加上if判断，这样我们就可以筛选出仅偶数的平方[x * x for x in range(1, 11) if x % 2 == 0]
还可以使用两层循环，可以生成全排列[m + n for m in 'ABC' for n in 'XYZ']
```python
print range(1, 11)
print [x * x for x in range(1, 11)]
print [x * x for x in range(1, 11) if x % 2 == 0]
print [m + n for m in 'ABC' for n in 'XYZ']
import os
print [d for d in os.listdir('.')]
```

##### **生成器**
> 通过列表生成式，我们可以直接创建一个列表。但是，受到内存限制，列表容量肯定是有限的。而且，创建一个包含100万个元素的列表，不仅占用很大的存储空间，如果我们仅仅需要访问前面几个元素，那后面绝大多数元素占用的空间都白白浪费了。
所以，如果列表元素可以按照某种算法推算出来，那我们是否可以在循环的过程中不断推算出后续的元素呢？这样就不必创建完整的list，从而节省大量的空间。在Python中，这种一边循环一边计算的机制，称为生成器（Generator）。
创建一个generator，有很多种方法。第一种方法很简单，只要把一个列表生成式的[]改成()，就创建了一个generator
```python
L = [x * x for x in range(10)]
print L
g = (x * x for x in range(10))
print g
```
> L是一个list，而g是一个generator
generator保存的是算法，每次调用next()，就计算出下一个元素的值，直到计算到最后一个元素，没有更多的元素时，抛出StopIteration的错误。
正确的方法是使用for循环，因为generator也是可迭代对象
```python
g = (x * x for x in range(10))
for n in g:
    print n
```

----------


### 函数式编程
##### **高阶函数**
变量可以指向函数
> 函数本身也可以赋值给变量，即：变量可以指向函数。
```python
f = abs
print f(-10)
```

函数名也是变量
> 把abs指向10后，就无法通过abs(-10)调用该函数了！因为abs这个变量已经不指向求绝对值函数了！
当然实际代码绝对不能这么写，这里是为了说明函数名也是变量。要恢复abs函数，请重启Python交互环境。
```python
abs = 10
print abs(-10)      # 此时abs不是原来的函数了
```

传入函数
> 既然变量可以指向函数，函数的参数能接收变量，那么一个函数就可以接收另一个函数作为参数，这种函数就称之为高阶函数。
```python
def add(x, y, f):
    return f(x) + f(y)
print add(-5, 6, abs)
```

map/reduce
> Python内建了map()和reduce()函数
map()函数接收两个参数，一个是函数，一个是序列，map将传入的函数依次作用到序列的每个元素，并把结果作为新的list返回
reduce把一个函数作用在一个序列[x1, x2, x3...]上，这个函数必须接收两个参数，reduce把结果继续和序列的下一个元素做累积计算，其效果就是：reduce(f, [x1, x2, x3, x4]) = f(f(f(x1, x2), x3), x4)

```python
def f(x):
    return x * x

print map(f, [1,2,3,4,5,6,7,8,9])

def add(x,y):
    return x + y

print reduce(add, [1,3,5,7,9])
```

> map/reduce一般配合使用

```python
def fn(x, y):
    return x * 10 + y

def char2num(s):
    return {'0': 0, '1': 1, '2': 2, '3': 3, '4': 4, '5': 5, '6': 6, '7': 7, '8': 8, '9': 9}[s]

print reduce(fn, map(char2num, '13579'))
```

filter
> Python内建的filter()函数用于过滤序列
和map()类似，filter()也接收一个函数和一个序列。和map()不同的时，filter()把传入的函数依次作用于每个元素，然后根据返回值是True还是False决定保留还是丢弃该元素。

```python
def is_odd(n):
    return n % 2 == 1

print filter(is_odd, [1, 2, 4, 5, 6, 9, 10, 15])

def not_empty(s):
    return s and s.strip()
    
print filter(not_empty, ['A','','B','','C'])
```

sorted
> 排序算法
排序也是在程序中经常用到的算法。无论使用冒泡排序还是快速排序，排序的核心是比较两个元素的大小。如果是数字，我们可以直接比较，但如果是字符串或者两个dict呢？直接比较数学上的大小是没有意义的，因此，比较的过程必须通过函数抽象出来。通常规定，对于两个元素x和y，如果认为x < y，则返回-1，如果认为x == y，则返回0，如果认为x > y，则返回1，这样，排序算法就不用关心具体的比较过程，而是根据比较结果直接排序。
> Python内置的sorted()函数就可以对list进行排序
> 还可以接收一个比较函数来实现自定义的排序。

```python
print sorted([36, 5, 12, 9, 21])

def reversed_cmp(x, y):
    if x > y:
        return -1
    if x < y:
        return 1
    return 0

print sorted([36, 5, 12, 9, 21], reversed_cmp)
```

##### **返回函数**
> 高阶函数除了可以接受函数作为参数外，还可以把函数作为结果值返回
通常情况下，求和的函数是这样定义的:

```python
def calc_sum(*args):
    ax = 0
    for n in args:
        ax = ax + n
    return ax
```

> 如果不需要立刻求和，而是在后面的代码中，根据需要再计算怎么办？可以不返回求和的结果，而是返回求和的函数！

```python
def lazy_sum(*args):
    def sum():
        ax = 0
        for n in args:
            ax = ax + n
        return ax
    return sum

f = lazy_sum(1, 3, 5, 7, 9)
print f()
```

> 在函数lazy_sum中又定义了函数sum，并且，内部函数sum可以引用外部函数lazy_sum的参数和局部变量，当lazy_sum返回函数sum时，相关参数和变量都保存在返回的函数中，这种称为“闭包（Closure）”的程序结构拥有极大的威力。

闭包
> 注意到返回的函数在其定义内部引用了局部变量args，所以，当一个函数返回了一个函数后，其内部的局部变量还被新函数引用，所以，闭包用起来简单，实现起来可不容易。
> 另一个需要注意的问题是，返回的函数并没有立刻执行，而是直到调用了f()才执行。我们来看一个例子：

```python
def count():
    fs = []
    for i in range(1, 4):
        def f():
             return i*i
        fs.append(f)
    return fs

f1, f2, f3 = count()

print f1()
print f2()
print f3()
```
> 实际结果是：全部都是9！原因就在于返回的函数引用了变量i，但它并非立刻执行。等到3个函数都返回时，它们所引用的变量i已经变成了3，因此最终结果为9。
> 返回闭包时牢记的一点就是：返回函数不要引用任何循环变量，或者后续会发生变化的变量。
> 如果一定要引用循环变量怎么办？方法是再创建一个函数，用该函数的参数绑定循环变量当前的值，无论该循环变量后续如何更改，已绑定到函数参数的值不变

```python
def count():
    fs = []
    for i in range(1, 4):
        def f(j):
            def g():
                return j*j
            return g
        fs.append(f(i))
    return fs

f1, f2, f3 = count()
print f1()
print f2()
print f3()
```

##### **匿名函数**
> 当我们在传入函数时，有些时候，不需要显式地定义函数，直接传入匿名函数更方便。
> 关键字lambda表示匿名函数
> 匿名函数有个限制，就是只能有一个表达式，不用写return，返回值就是该表达式的结果
> 用匿名函数有个好处，因为函数没有名字，不必担心函数名冲突。此外，匿名函数也是一个函数对象，也可以把匿名函数赋值给一个变量，再利用变量来调用该函数：

```python
print map(lambda x: x * x, [1, 2, 3, 4, 5, 6, 7, 8, 9])

f = lambda x: x * x
print f(5)

def build(x, y):
    return lambda: x * x + y * y
print build(3, 4)
```

##### **装饰器**
> 在面向对象（OOP）的设计模式中，decorator被称为装饰模式。OOP的装饰模式需要通过继承和组合来实现，而Python除了能支持OOP的decorator外，直接从语法层次支持decorator。Python的decorator可以用函数实现，也可以用类实现。
> decorator可以增强函数的功能，定义起来虽然有点复杂，但使用起来非常灵活和方便。
> Python内置的functools.wraps就是装饰器

```python
import time
def now():
    print time.time()
```
> 我们要增强now()函数的功能，比如，在函数调用前后自动打印日志，但又不希望修改now()函数的定义，这种在代码运行期间动态增加功能的方式，称之为“装饰器”（Decorator）
> 借助Python的@语法，把decorator置于函数的定义处

```python
import time

def log(func):
    def wrapper(*args, **kw):
        print 'call %s():' % func.__name__
        return func(*args, **kw)
    return wrapper

@log
def now():
    print time.time()

# 把@log放到now()函数的定义处，相当于执行了语句now = log(now)
print now()  
```

```python
import time

def log(text):
    def decorator(func):
        def wrapper(*args, **kw):
            print '%s %s():' % (text, func.__name__)
            return func(*args, **kw)
        return wrapper
    return decorator

@log('execute')
def now():
    print time.time()

# 把@log放到now()函数的定义处，相当于执行了语句now = log('execute')(now)
print now()  
```

> 以上两种decorator的定义都没有问题，但还差最后一步。因为我们讲了函数也是对象，它有__name__等属性，但你去看经过decorator装饰之后的函数，它们的__name__已经从原来的'now'变成了'wrapper'：
> 需要把原始函数的__name__等属性复制到wrapper()函数中，否则，有些依赖函数签名的代码执行就会出错。
> 不需要编写wrapper.__name__ = func.__name__这样的代码，Python内置的functools.wraps就是干这个事的
> 一个完整的decorator的写法如下:

```python
import functools

# 不带参数
def log(func):
    @functools.wraps(func)
    def wrapper(*args, **kw):
        print 'call %s():' % func.__name__
        return func(*args, **kw)
    return wrapper

# 带参数
def log(text):
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kw):
            print '%s %s():' % (text, func.__name__)
            return func(*args, **kw)
        return wrapper
    return decorator
```


##### **偏函数**
> Python的functools模块提供了很多有用的功能，其中一个就是偏函数（Partial function）
> int()函数可以把字符串转换为整数，当仅传入字符串时，int()函数默认按十进制转换:
> 但int()函数还提供额外的base参数，默认值为10。如果传入base参数，就可以做N进制的转换
> 假设要转换大量的二进制字符串，每次都传入int(x, base=2)非常麻烦，于是，我们想到，可以定义一个int2()的函数，默认把base=2传进去：

```python
print int('12345')
print int('12345', base=8)

def int2(x, base=2):
    return int(x, base)
print int2('1000000')
```

> functools.partial就是帮助我们创建一个偏函数的，不需要我们自己定义int2()

```python
import functools

int2 = functools.partial(int, base=2)
print int2('1010101')
```
> 当函数的参数个数太多，需要简化时，使用functools.partial可以创建一个新的函数，这个新函数可以固定住原函数的部分参数，从而在调用时更简单


----------
### 模块
> 为了编写可维护的代码，我们把很多函数分组，分别放到不同的文件里，这样，每个文件包含的代码就相对较少，很多编程语言都采用这种组织代码的方式。在Python中，一个.py文件就称之为一个模块（Module）

##### **使用模块**
> Python本身就内置了很多非常有用的模块，只要安装完毕，这些模块就可以立刻使用。
> 以内建的sys模块为例，编写一个hello的模块：

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

' a test module '

__author__ = 'Michael Liao'

import sys

def test():
    args = sys.argv
    if len(args)==1:
        print 'Hello, world!'
    elif len(args)==2:
        print 'Hello, %s!' % args[1]
    else:
        print 'Too many arguments!'

if __name__=='__main__':
    test()
```

> 第1行注释可以让这个hello.py文件直接在Unix/Linux/Mac上运行；
> 第2行注释表示.py文件本身使用标准UTF-8编码；
> 第4行是一个字符串，表示模块的文档注释，任何模块代码的第一个字符串都被视为模块的文档注释；
> 第6行使用__author__变量把作者写进去，这样当你公开源代码后别人就可以瞻仰你的大名；
> 以上就是Python模块的标准文件模板，当然也可以全部删掉不写，但是，按标准办事肯定没错。

别名
> Python标准库一般会提供StringIO和cStringIO两个库，这两个库的接口和功能是一样的，但是cStringIO是C写的，速度更快，所以，你会经常看到这样的写法
```python
try:
    import cStringIO as StringIO
except ImportError: # 导入失败会捕获到ImportError
    import StringIO
```

作用域
> 在一个模块中，我们可能会定义很多函数和变量，但有的函数和变量我们希望给别人使用，有的函数和变量我们希望仅仅在模块内部使用。在Python中，是通过_前缀来实现的。

> 正常的函数和变量名是公开的（public），可以被直接引用，比如：abc，x123，PI等；

> 类似__xxx__这样的变量是特殊变量，可以被直接引用，但是有特殊用途，比如上面的__author__，__name__就是特殊变量，hello模块定义的文档注释也可以用特殊变量__doc__访问，我们自己的变量一般不要用这种变量名；

> 类似_xxx和__xxx这样的函数或变量就是非公开的（private），不应该被直接引用，比如_abc，__abc等；

> 之所以我们说，private函数和变量“不应该”被直接引用，而不是“不能”被直接引用，是因为Python并没有一种方法可以完全限制访问private函数或变量，但是，从编程习惯上不应该引用private函数或变量。


##### **安装第三方模块**
> 在Python中，安装第三方模块，是通过setuptools这个工具完成的。Python有两个封装了setuptools的包管理工具：easy_install和pip。目前官方推荐使用pip。
> 如果你正在使用Mac或Linux，安装pip本身这个步骤就可以跳过了。
> 如果你正在使用Windows，请参考安装Python一节的内容，确保安装时勾选了pip和Add python.exe to Path。

```
pip install xxx
```
    
##### **使用__future__**
> 由于Python是由社区推动的开源并且免费的开发语言，不受商业公司控制，因此，Python的改进往往比较激进，不兼容的情况时有发生。Python为了确保你能顺利过渡到新版本，特别提供了__future__模块，让你在旧的版本中试验新版本的一些特性。


----------
### 面向对象编程
> 面向对象编程——Object Oriented Programming，简称OOP，是一种程序设计思想。OOP把对象作为程序的基本单元，一个对象包含了数据和操作数据的函数。

##### **类和实例**
> 在Python中，定义类是通过class关键字：

```python
class Student(object):

    def __init__(self, name, score):
        self.name = name
        self.score = score

    def print_score(self):
        print '%s: %s' % (self.name, self.score)
        
    def get_grade(self):
        if self.score >= 90:
            return 'A'
        elif self.score >= 60:
            return 'B'
        else:
            return 'C'

bart = Student('Bart Simpson', 59)
bart.age = 8
print bart.print_score()
print bart.get_grade()
print bart.age
```

> __init__方法的第一个参数永远是self，表示创建的实例本身，因此，在__init__方法内部，就可以把各种属性绑定到self，因为self就指向创建的实例本身。
> 类是创建实例的模板，而实例则是一个一个具体的对象，各个实例拥有的数据都互相独立，互不影响；
> 方法就是与实例绑定的函数，和普通函数不同，方法可以直接访问实例的数据；
> 通过在实例上调用方法，我们就直接操作了对象内部的数据，但无需知道方法内部的实现细节。
> 和静态语言不同，Python允许对实例变量绑定任何数据，也就是说，对于两个实例变量，虽然它们都是同一个类的不同实例，但拥有的变量名称都可能不同：


##### **访问限制**
> 在Class内部，可以有属性和方法，而外部代码可以通过直接调用实例变量的方法来操作数据，这样，就隐藏了内部的复杂逻辑。
> 如果要让内部属性不被外部访问，可以把属性的名称前加上两个下划线__，在Python中，实例的变量名如果以__开头，就变成了一个私有变量（private），只有内部可以访问，外部不能访问，

```python
class Student(object):

    def __init__(self, name, score):
        self.__name = name
        self.__score = score

    def print_score(self):
        print '%s: %s' % (self.__name, self.__score)
```
> 对于外部代码来说，没什么变动，但是已经无法从外部访问实例变量.__name和实例变量.__score了
> 在Python中，变量名类似__xxx__的，也就是以双下划线开头，并且以双下划线结尾的，是特殊变量，特殊变量是可以直接访问的，不是private变量，所以，不能用__name__、__score__这样的变量名。
> 有些时候，你会看到以一个下划线开头的实例变量名，比如_name，这样的实例变量外部是可以访问的，但是，按照约定俗成的规定，当你看到这样的变量时，意思就是，“虽然我可以被访问，但是，请把我视为私有变量，不要随意访问”。
> 双下划线开头的实例变量是不是一定不能从外部访问呢？其实也不是。不能直接访问__name是因为Python解释器对外把__name变量改成了_Student__name，所以，仍然可以通过_Student__name来访问__name变量。但是强烈建议你不要这么干，因为不同版本的Python解释器可能会把__name改成不同的变量名
> Python本身没有任何机制阻止你干坏事，一切全靠自觉。


##### **继承和多态**
> 继承可以把父类的所有功能都直接拿过来，这样就不必重零做起，子类只需要新增自己特有的方法，也可以把父类不适合的方法覆盖重写；

> 有了继承，才能有多态。在调用类实例方法的时候，尽量把变量视作父类类型，这样，所有子类类型都可以正常被接收；

> 旧的方式定义Python类允许不从object类继承，但这种编程方式已经严重不推荐使用。任何时候，如果没有合适的类可以继承，就继承自object类。

##### **获取对象信息**
使用type()
```python
print type(123)
print type('str')
print type(None)

# type()函数返回的是什么类型呢？它返回type类型。如果我们要在if语句中判断，就需要比较两个变量的type类型是否相同
# Python把每种type类型都定义好了常量，放在types模块里
print type(123)==type(456)
print type('abc')==types.StringType
print type(u'abc')==types.UnicodeType
print type([])==types.ListType
print type(str)==types.TypeType
```

> 所有类型本身的类型就是TypeType

使用isinstance()

> 能用type()判断的基本类型也可以用isinstance()判断：

```python
print isinstance('a', str)
print isinstance(u'a', unicode)
```

使用dir()

> 如果要获得一个对象的所有属性和方法，可以使用dir()函数，它返回一个包含字符串的list，比如，获得一个str对象的所有属性和方法：

```python
print dir('ABC')
```

> 仅仅把属性和方法列出来是不够的，配合getattr()、setattr()以及hasattr()，我们可以直接操作一个对象的状态：

```python
class MyObject(object):
    def __init__(self):
        self.x = 9
    def power(self):
        return self.x * self.x

obj = MyObject()
if hasattr(obj, 'x'):
    print obj.x
if hasattr(obj, 'y'):
    setattr(obj, 'y', 19)
    print getattr(obj, 'y')
```

----------
### 面向对象高级编程
##### **使用__slots__**
> 限制class的属性怎么办？比如，只允许对Student实例添加name和age属性。
> 为了达到限制的目的，Python允许在定义class的时候，定义一个特殊的__slots__变量，来限制该class能添加的属性

```python
class Student(object):
    __slots__ = ('name', 'age') # 用tuple定义允许绑定的属性名称
    
s = Student()
s.name = 'Michael' # 绑定属性'name'
s.age = 25 # 绑定属性'age'
# 由于'score'没有被放到__slots__中，所以不能绑定score属性，试图绑定score将得到AttributeError的错误
#s.score = 99 
```

> 定义的属性__slots__仅对当前类起作用，对继承的子类是不起作用的


##### **使用@property**
> Python内置的@property装饰器就是负责把一个方法变成属性调用的

```python
class Student(object):

    @property
    def score(self):
        return self._score

    @score.setter
    def score(self, value):
        if not isinstance(value, int):
            raise ValueError('score must be an integer!')
        if value < 0 or value > 100:
            raise ValueError('score must between 0 ~ 100!')
        self._score = value
    
s = Student()
s.score = 60   # OK，实际转化为s.set_score(60)
print s.score  # OK，实际转化为s.get_score()
```

> 把一个getter方法变成属性，只需要加上@property就可以了
> @property本身又创建了另一个装饰器@score.setter，负责把一个setter方法变成属性赋值


> 还可以定义只读属性，只定义getter方法，不定义setter方法就是一个只读属性

```python
class Student(object):

    @property
    def birth(self):
        return self._birth

    @birth.setter
    def birth(self, value):
        self._birth = value

    @property
    def age(self):
        return 2014 - self._birth

s = Student()
s.birth = 1987
print s.birth
print s.age
```

##### **多重继承**
> Mixin的目的就是给一个类增加多个功能，这样，在设计类的时候，我们优先考虑通过多重继承来组合多个Mixin的功能，而不是设计多层次的复杂的继承关系。

> Python允许使用多重继承，Mixin就是一种常见的设计。
> 只允许单一继承的语言（如Java）不能使用Mixin的设计。

> Python自带的很多库也使用了Mixin

```python
# 多进程模式的TCP服务
class MyTCPServer(TCPServer, ForkingMixin):
    pass

# 多线程模式的UDP服务
class MyUDPServer(UDPServer, ThreadingMixin):
    pass
```

##### **定制类**
**__str__返回用户看到的字符串**
**__repr__返回程序开发者看到的字符串**
**__iter__返回一个迭代对象**

```python
class Fib(object):
    def __init__(self):
        self.a, self.b = 0, 1 # 初始化两个计数器a，b

    def __iter__(self):
        return self # 实例本身就是迭代对象，故返回自己

    def next(self):
        self.a, self.b = self.b, self.a + self.b # 计算下一个值
        if self.a > 100000: # 退出循环的条件
            raise StopIteration();
        return self.a # 返回下一个值
    
    def __getitem__(self, n):
        if isinstance(n, int):
            a, b = 1, 1
            for x in range(n):
                a, b = b, a + b
            return a
        if isinstance(n, slice):
            start = n.start
            stop = n.stop
            a, b = 1, 1
            L = []
            for x in range(stop):
                if x >= start:
                    L.append(a)
                a, b = b, a + b
            return L
```

**__getitem__获取元素或切片**
**__setitem__设置元素**
**__delitem__删除元素**
**__getattr__动态返回一个属性**
**__call__调用实例本身**
> 通过callable()函数，我们就可以判断一个对象是否是“可调用”对象。

```python
print callable(max)
print callable('string')
print callable(None)
```

> 更多参考 https://docs.python.org/2/reference/datamodel.html#special-method-names


##### **使用元类**
type()
> class的定义是运行时动态创建的，而创建class的方法就是使用type()函数。

```python
# 定义函数
def fn(self, name='world'):
    print('Hello, %s.' % name)

Hello = type('Hello', (object,), dict(hello=fn)) # 创建Hello class

h = Hello()
h.hello
print(type(Hello))
print(type(h))
```

> 要创建一个class对象，type()函数依次传入3个参数：
 1. class的名称；
 2. 继承的父类集合，注意Python支持多重继承，如果只有一个父类，别忘了tuple的单元素写法；
 3. class的方法名称与函数绑定，这里我们把函数fn绑定到方法名hello上。

metaclass
> 除了使用type()动态创建类以外，要控制类的创建行为，还可以使用metaclass。
> metaclass，直译为元类，简单的解释就是：
> 当我们定义了类以后，就可以根据这个类创建出实例，所以：先定义类，然后创建实例。
> 但是如果我们想创建出类呢？那就必须根据metaclass创建出类，所以：先定义metaclass，然后创建类。
> 连接起来就是：先定义metaclass，就可以创建类，最后创建实例。
> 所以，metaclass允许你创建类或者修改类。换句话说，你可以把类看成是metaclass创建出来的“实例”。

> 我们先看一个简单的例子，这个metaclass可以给我们自定义的MyList增加一个add方法：
> 定义ListMetaclass，按照默认习惯，metaclass的类名总是以Metaclass结尾，以便清楚地表示这是一个metaclass：

```python
# metaclass是创建类，所以必须从`type`类型派生：
class ListMetaclass(type):
    def __new__(cls, name, bases, attrs):
        attrs['add'] = lambda self, value: self.append(value)
        return type.__new__(cls, name, bases, attrs)

class MyList(list):
    __metaclass__ = ListMetaclass # 指示使用ListMetaclass来定制类
    
L = MyList()
L.add(1)
print L
```

> 当我们写下 \_\_metaclass\_\_ = ListMetaclass语句时，魔术就生效了，它指示Python解释器在创建MyList时，要通过ListMetaclass.\_\_new\_\_()来创建，在此，我们可以修改类的定义，比如，加上新的方法，然后，返回修改后的定义。
> \_\_new\_\_()方法接收到的参数依次是：
1. 当前准备创建的类的对象；
2. 类的名字；
3. 类继承的父类集合；
4. 类的方法集合。



----------
### 错误、调试和测试
##### **错误处理**
> 高级语言通常都内置了一套try...except...finally...的错误处理机制，Python也不例外

```python
try:
    print 'try...'
    r = 10 / int('a')
    print 'result:', r
except ValueError, e:
    print 'ValueError:', e
except ZeroDivisionError, e:
    print 'ZeroDivisionError:', e
finally:
    print 'finally...'
print 'END'
```

> 此外，如果没有错误发生，可以在except语句块后面加一个else，当没有错误发生时，会自动执行else语句：

```python
try:
    print 'try...'
    r = 10 / int('a')
    print 'result:', r
except ValueError, e:
    print 'ValueError:', e
except ZeroDivisionError, e:
    print 'ZeroDivisionError:', e
else:
    print 'no error!'
finally:
    print 'finally...'
print 'END'
```

> Python的错误其实也是class，所有的错误类型都继承自BaseException
> 常见的错误类型和继承关系看这里：https://docs.python.org/2/library/exceptions.html#exception-hierarchy

记录错误
> python 内置的logging模块可以非常容易地记录错误信息:
```python
try:
    return 10 / int('0')
except StandardError, e:
    logging.exception(e)
```

抛出错误
> 因为错误是class，捕获一个错误就是捕获到该class的一个实例。因此，错误并不是凭空产生的，而是有意创建并抛出的。Python的内置函数会抛出很多类型的错误，我们自己编写的函数也可以抛出错误。
> 如果要抛出错误，首先根据需要，可以定义一个错误的class，选择好继承关系，然后，用raise语句抛出一个错误的实例：

```python
class FooError(StandardError):
    pass

def foo(s):
    n = int(s)
    if n==0:
        raise FooError('invalid value: %s' % s)
    return 10 / n
```

##### **调试**
> 第一种方法简单直接粗暴有效，就是用print把可能有问题的变量打印出来看看
> 第二种方法用print来辅助查看的地方，都可以用断言（assert）来替代

```python
def foo(s):
    n = int(s)
    assert n != 0, 'n is zero!'
    return 10 / n

def main():
    foo('0')
```

> assert的意思是，表达式n != 0应该是True，否则，后面的代码就会出错。
> 第三种方法logging，logging允许你指定记录信息的级别，有debug，info，warning，error等几个级别
> 第四种方式是启动Python的调试器pdb
> 最后，如果要比较爽地设置断点、单步执行，就需要一个支持调试功能的IDE。目前比较好的Python IDE有PyCharm

##### **单元测试**
> 编写单元测试，我们需要引入Python自带的unittest模块。编写单元测试时，我们需要编写一个测试类，从unittest.TestCase继承。
> 以test开头的方法就是测试方法，不以test开头的方法不被认为是测试方法，测试的时候不会被执行。
> 对每一类测试都需要编写一个test_xxx()方法。由于unittest.TestCase提供了很多内置的条件判断，我们只需要调用这些方法就可以断言输出是否是我们所期望的。最常用的断言就是assertEquals()：
> 另一种重要的断言就是期待抛出指定类型的Error，比如通过d['empty']访问不存在的key时，断言会抛出KeyError：

```python
class Dict(dict):

    def __init__(self, **kw):
        super(Dict, self).__init__(**kw)

    def __getattr__(self, key):
        try:
            return self[key]
        except KeyError:
            raise AttributeError(r"'Dict' object has no attribute '%s'" % key)

    def __setattr__(self, key, value):
        self[key] = value
        

import unittest

from mydict import Dict

class TestDict(unittest.TestCase):
    def setUp(self):
        print 'setUp...'

    def tearDown(self):
        print 'tearDown...'

    def test_init(self):
        d = Dict(a=1, b='test')
        self.assertEquals(d.a, 1)
        self.assertEquals(d.b, 'test')
        self.assertTrue(isinstance(d, dict))

    def test_key(self):
        d = Dict()
        d['key'] = 'value'
        self.assertEquals(d.key, 'value')

    def test_attr(self):
        d = Dict()
        d.key = 'value'
        self.assertTrue('key' in d)
        self.assertEquals(d['key'], 'value')

    def test_keyerror(self):
        d = Dict()
        with self.assertRaises(KeyError):
            value = d['empty']

    def test_attrerror(self):
        d = Dict()
        with self.assertRaises(AttributeError):
            value = d.empty
```

运行单元测试
> 最简单的运行方式:是在mydict_test.py的最后加上两行代码

```python
if __name__ == '__main__':
    unittest.main()
```

> 另一种更常见的方法是在命令行通过参数-m unittest直接运行单元测试：

```
python -m unittest mydict_test
```

setUp与tearDown
> 单元测试中编写两个特殊的setUp()和tearDown()方法。这两个方法会分别在每调用一个测试方法的前后分别被执行。


##### **文档测试**

```python
class Dict(dict):
    '''
    Simple dict but also support access as x.y style.

    >>> d1 = Dict()
    >>> d1['x'] = 100
    >>> d1.x
    100
    >>> d1.y = 200
    >>> d1['y']
    200
    >>> d2 = Dict(a=1, b=2, c='3')
    >>> d2.c
    '3'
    >>> d2['empty']
    Traceback (most recent call last):
        ...
    KeyError: 'empty'
    >>> d2.empty
    Traceback (most recent call last):
        ...
    AttributeError: 'Dict' object has no attribute 'empty'
    '''
    def __init__(self, **kw):
        super(Dict, self).__init__(**kw)

    def __getattr__(self, key):
        try:
            return self[key]
        except KeyError:
            raise AttributeError(r"'Dict' object has no attribute '%s'" % key)

    def __setattr__(self, key, value):
        self[key] = value

if __name__=='__main__':
    import doctest
    doctest.testmod()
```
> doctest非常有用，不但可以用来测试，还可以直接作为示例代码。通过某些文档生成工具，就可以自动把包含doctest的注释提取出来。用户看文档的时候，同时也看到了doctest。

