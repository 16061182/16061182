---
title: matplotlib绘图示例以及一些numpy函数解析
categories:  
- 笔记 
tags:
- 绘图
- numpy
- python
---

## matplotlib绘图示例以及一些numpy函数解析

#### matplotlib绘图示例代码

```python
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
sns.set(color_codes=True)
```

```python
def show_image(len_record):
    x = ['0~4','5~9','10~14','15~19','20~24','25~29','30~34','35~39','40~44','45~49','50~54','55~59','60~64','>=65']
    y = [0] * 14
    plt.figure(figsize=(8, 6))
    for record in len_record:
        ans = int(record / 5)
        if ans >= 13:
            ans = 13
        y[ans] += 1
    x = np.array(x)
    y = np.array(y)
    width = 0.5
    '''
    plt.bar()参数： 
1. left：x轴的位置序列，一般采用arange函数产生一个序列； 
2. height：y轴的数值序列，也就是柱形图的高度，一般就是我们需要展示的数据； 
3. alpha：透明度 
4. width：为柱形图的宽度，一般这是为0.8即可； 
5. color或facecolor：柱形图填充的颜色； 
6. edgecolor：图形边缘颜色 
7. label：解释每个图像代表的含义 
8. linewidth or linewidths or lw：边缘or线的宽度
    '''
    index = np.arange(len(x))
    plt.bar(index, y, width, color="#87CEFA")
    plt.xlabel('length') #x轴
    plt.ylabel('quantity')  # y轴
    plt.title('total:' + str(len(len_record)))  # 图像的名称
    plt.xticks(index, x, fontsize=8)  # 将横坐标用cell替换,fontsize用来调整字体的大小
    plt.legend()  # 显示label
    # for i in range(len(x)):
    #     plt.text(x[i], y[i], y[i], ha='center', va='bottom')
    for xx, yy in zip(index, y):
        plt.text(xx, yy + 0.1, str(yy), ha='center', va='bottom')
    plt.show()
```

#### numpy函数
- np.linspace()

```python
Parameters(参数):	
start : 序列的起始点.
stop : 序列的结束点
num : 生成的样本数，默认是50。必须是非负。
endpoint : 如果True，stop是最后一个样本。否则，它不包括在内。默认为True。
retstep :  如果True,返回 (向量, 步长)
dtype : 
```

- np.arange

```python
>>>range(1,5)
range(1,5)
>>>tuple(range(1, 5))
(1, 2, 3, 4)
>>>list(range(1, 5))
[1, 2, 3, 4]


>>>r = range(1, 5)
>>>type(r)
<class 'range'>

>>>for  i in range(1, 5):
...    print(i)
1
2
3
4

>>> np.arange(1, 5)
array([1, 2, 3, 4])

>>>range(1, 5, .1)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'float' object cannot be interpreted as an integer

>>>np.arange(1, 5, .5)
array([ 1. ,  1.5,  2. ,  2.5,  3. ,  3.5,  4. ,  4.5])

>>>range(1, 5, 2)
>>>for i in range(1, 5, 2):
...    print(i)
1
3

>>for i in np.arange(1, 5):
...    print(i)
1
2
3
4
```

