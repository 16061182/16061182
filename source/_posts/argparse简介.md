---
title: argparse简介
categories:  
- 原创
- 教程
tags:
- argparse
- python
---

## argparse简介
本文为博主原创，转载请注明出处！

argparse是一个**命令行参数解析**模块，还是挺有用的，下面介绍一些基本用法。

### 位置参数
test.py：
```python
import argparse
parser = argparse.ArgumentParser()
parser.description = '计算乘积'
parser.add_argument("ParA", help='我是A', type=int)
parser.add_argument("ParB", help='我是B', type=int)
args = parser.parse_args()
if args.ParA:
    print("A is",args.ParA)
if args.ParB:
    print("B is",args.ParB)
if args.ParA and args.ParB:
    print("A和B的乘积",args.ParA*args.ParB)
```
命令行：
```
$ python test.py 5 4
A is 5
B is 4
A和B的乘积 20
```
注：
- 如果输入命令`python test.py --help`，会给出本程序所需所有参数的帮助信息，在本例中结果为：
```
usage: test.py [-h] ParA ParB

计算乘积

positional arguments:
  ParA        我是A
  ParB        我是B

optional arguments:
  -h, --help  show this help message and exit
```
- `.add_argument`中的`ParA`就是位置参数，在命令行输入命令的时候会根据参数的顺序为`ParA`和`ParB`赋值，**位置参数不全的话会报错**。
- 若不指定`type = int`，会默认输入参数为str。

------

### 可选参数
test.py：
```python
import argparse
parser = argparse.ArgumentParser()
parser.description = '计算乘积'
parser.add_argument("--ParA", '-a', help='我是A', type=int)
parser.add_argument('-b', "--ParB", help='我是B', type=int)
parser.add_argument('-c', "--ParC", help='我是C', action='store_true')
args = parser.parse_args()
if args.ParA:
    print("A is",args.ParA)
if args.ParB:
    print("B is",args.ParB)
if args.ParC:
    print("True")
```
命令行：
```
$ python test.py --ParB 5 -a 4 --ParC
A is 4
B is 5
True
```
注：
- 把`ParA`改为`--ParA`之后，就变成了可选参数，相比位置参数，可选参数**不要求顺序**、**不要求输入全部参数**。
- 命令行中可以用`-a`和`-b`可以代替`--ParA`和`--ParB`，`-aa`代替`--ParA --ParA`，使输入简化。
- `action='store_true'`使`--ParC`不接收值，该参数只起到通过`if args.ParC`判断是非的作用。如果命令行中写了`--ParC`，`args.ParC`的值为True。

------

### 位置参数和可选参数结合

（1）test.py：
```python
import argparse
parser = argparse.ArgumentParser()
parser.add_argument("ParA", help='我是A', type=int)
parser.add_argument('-b', "--ParB", help='我是B', type=int, choices=[0, 1, 2])
args = parser.parse_args()
answer = args.ParA ** 2
if args.ParB == 2:
    print("the square of {} equals {}".format(args.ParA, answer))
elif args.ParB == 1:
    print("{}^2 == {}".format(args.ParA, answer))
else:
    print(answer)
```
命令行：
```
$ python test.py 4 -b 2
the square of 4 equals 16

$ python test.py -b 1 4
4^2 == 16

$ python test.py -b 3 4
usage: test.py [-h] [--ParA PARA] [-b {0,1,2}]
test.py: error: argument -b/--ParB: invalid choice: 3 (choose from 0, 1, 2)

$ python test.py -h
usage: test.py [-h] [-b {0,1,2}] ParA

positional arguments:
  ParA                  我是A

optional arguments:
  -h, --help            show this help message and exit
  -b {0,1,2}, --ParB {0,1,2}
                        我是B
```
注：
- `ParA`和`ParB`的位置可以互换。
- `choices=[0, 1, 2]`为`ParB`规定范围。

（2）test.py：

```python
import argparse
parser = argparse.ArgumentParser()
parser.add_argument("ParA", help='我是A', type=int)
parser.add_argument('-b', "--ParB", help='我是B', action='count')
args = parser.parse_args()
answer = args.ParA ** 2
if args.ParB == 2:
    print("the square of {} equals {}".format(args.ParA, answer))
elif args.ParB == 1:
    print("{}^2 == {}".format(args.ParA, answer))
else:
    print(answer)
```
命令行：
```
$ python test.py 4
16

$ python test.py 4 -b
4^2 == 16

$ python test.py 4 -bb
the square of 4 equals 16

$ python test.py 4 --ParB --ParB
the square of 4 equals 16
```
注：
- `action='count'`和`action='store_true'`类似，该输入不需要具体值，而是根据命令行输入的该参数名的数量来决定该参数的值。
- 对上述(2)test.py进行修改，在`else`前添加如下代码，则不输入`--ParB`时会报错，因为此时`args.ParB`是None而不是值为0。
```
elif args.ParB > 2:
    print('ParB > 2')
```
```
$ python test.py 4
Traceback (most recent call last):
  File "test.py", line 11, in <module>
    elif args.ParB > 2:
TypeError: '>' not supported between instances of 'NoneType' and 'int'
```
- 若想让上述情况不报错，可以设置`args.ParB`默认值为0，只需`parser.add_argument('-b', "--ParB", help='我是B', default=0, action='count')`。

------

### 矛盾的选项
test.py：
```python
import argparse
parser = argparse.ArgumentParser()
group = parser.add_mutually_exclusive_group()
group.add_argument("-t", "--true", action="store_true")
group.add_argument("-f", "--false", action="store_true")
parser.add_argument("ParA", help='我是A', type=int)
parser.add_argument("ParB", help='我是B', type=int)
args = parser.parse_args()
answer = args.ParA * args.ParB
if args.true:
    print('true', answer)
elif args.false:
    print('false', answer)
else:
    print('else', answer)
```
命令行：
```
$ python test.py 4 5 -t
true 20

$ python test.py 4 5 -f
false 20

$ python test.py 4 5 -tf
usage: test.py [-h] [-t | -f] ParA ParB
test.py: error: argument -f/--false: not allowed with argument -t/--true
```
注：
- `parser.add_mutually_exclusive_group()`内的参数是相互冲突的，在命令行中输入其中一个，就不能输入其他的。

------

### 写在最后
argparse模块还有很多其他的功能，转到[argparse](https://docs.python.org/3.6/library/argparse.html#module-argparse)以查看更多内容。
参考文章：

- [https://www.jianshu.com/p/00425f6c0936](https://www.jianshu.com/p/00425f6c0936)
- [https://docs.python.org/3.6/howto/argparse.html#introducing-optional-arguments](https://docs.python.org/3.6/howto/argparse.html#introducing-optional-arguments)