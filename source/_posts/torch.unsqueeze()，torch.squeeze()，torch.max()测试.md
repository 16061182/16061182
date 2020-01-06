---
title: torch.unsqueeze()，torch.squeeze()，torch.max()测试
categories:  
- 原创
- 笔记
tags:
- torch
- python
---

## torch.unsqueeze()，torch.squeeze()，torch.max()测试
本文为博主原创，转载请注明出处！

- **输入**

```python
import torch
a = [
    [1, 2, 3, 4],
    [5, 6, 7, 8],
    [9, 10, 11, 12]
]
a = torch.LongTensor(a)
aa = [[
    [1, 2, 3, 4],
    [5, 6, 7, 8],
    [9, 10, 11, 12]
]]
aa = torch.LongTensor(aa)
aaa = [
[
    [1, 2, 3, 4],
    [5, 6, 7, 8],
    [9, 10, 11, 12]
],
[
    [9, 10, 11, 12],
    [1, 2, 3, 4],
    [5, 6, 7, 8]
]
]
aaa = torch.LongTensor(aaa)
print(aaa.size())
'''
[in]print(a.size())
[out]torch.Size([3, 4])
[in]print(aa.size())
[out]torch.Size([1, 3, 4])
[in]print(aaa.size())
[out]torch.Size([2, 3, 4])
'''
# unsqueeze可作为维度的自然数范围是[0,矩阵层数=2]
print('unsqueeze, dim=0:')
b = torch.unsqueeze(a, dim=0)
print(b)
print('unsqueeze, dim=1:')
b = torch.unsqueeze(a, dim=1)
print(b)
print('unsqueeze, dim=2:')
b = torch.unsqueeze(a, dim=2)
print(b)
print('unsqueeze, dim=-1:')
b = torch.unsqueeze(a, dim=-1)
print(b)
print('*'*20)

# squeeze可作为维度的自然数范围是[0,矩阵层数-1=2]
print('squeeze, dim=0:') # 去除最外层
c = torch.squeeze(aa, dim=0)
print(c)
print('squeeze, dim=1:') # 无作用
c = torch.squeeze(aa, dim=1)
print(c)
print('squeeze, dim=2:') # 无作用
c = torch.squeeze(aa, dim=2)
print(c)
print('squeeze, dim=-1:') # 无作用
c = torch.squeeze(aa, dim=-1)
print(c)
print('squeeze, dim=-2:') # 无作用
c = torch.squeeze(aa, dim=-2)
print(c)
print('*'*20)
print('squeeze, dim=-3:') # 去除最外层
c = torch.squeeze(aa, dim=-3)
print(c)
print('*'*20)

# max可作为维度的自然数范围是[0,矩阵层数-1=2]
d = torch.max(aaa)
print(d)
print('max, dim=0:')
d, _ = torch.max(aaa, dim=0) # size_d:3 x 4，按第一维求最大
print(d)
print('max, dim=1:')
d, _ = torch.max(aaa, dim=1) # size_d:2 x 4，按第二维求最大
print(d)
print('max, dim=2:')
d, _ = torch.max(aaa, dim=2) # size_d:2 x 3，按第三维求最大
print(d)
print('max, dim=-1:')
d, _ = torch.max(aaa, dim=-1) # equivalent to dim=2
print(d)
print('max, dim=-2:')
d, _ = torch.max(aaa, dim=-2) # equivalent to dim=1
print(d)
print('max, dim=-3:')
d, _ = torch.max(aaa, dim=-3) # equivalent to dim=0
print(d)
```

- **输出**
```python
unsqueeze, dim=0:
tensor([[[ 1,  2,  3,  4],
         [ 5,  6,  7,  8],
         [ 9, 10, 11, 12]]])
unsqueeze, dim=1:
tensor([[[ 1,  2,  3,  4]],

        [[ 5,  6,  7,  8]],

        [[ 9, 10, 11, 12]]])
unsqueeze, dim=2:
tensor([[[ 1],
         [ 2],
         [ 3],
         [ 4]],

        [[ 5],
         [ 6],
         [ 7],
         [ 8]],

        [[ 9],
         [10],
         [11],
         [12]]])
unsqueeze, dim=-1:
tensor([[[ 1],
         [ 2],
         [ 3],
         [ 4]],

        [[ 5],
         [ 6],
         [ 7],
         [ 8]],

        [[ 9],
         [10],
         [11],
         [12]]])
********************
squeeze, dim=0:
tensor([[ 1,  2,  3,  4],
        [ 5,  6,  7,  8],
        [ 9, 10, 11, 12]])
squeeze, dim=1:
tensor([[[ 1,  2,  3,  4],
         [ 5,  6,  7,  8],
         [ 9, 10, 11, 12]]])
squeeze, dim=2:
tensor([[[ 1,  2,  3,  4],
         [ 5,  6,  7,  8],
         [ 9, 10, 11, 12]]])
squeeze, dim=-1:
tensor([[[ 1,  2,  3,  4],
         [ 5,  6,  7,  8],
         [ 9, 10, 11, 12]]])
squeeze, dim=-2:
tensor([[[ 1,  2,  3,  4],
         [ 5,  6,  7,  8],
         [ 9, 10, 11, 12]]])
********************
squeeze, dim=-3:
tensor([[ 1,  2,  3,  4],
        [ 5,  6,  7,  8],
        [ 9, 10, 11, 12]])
********************
tensor(12)
max, dim=0:
tensor([[ 9, 10, 11, 12],
        [ 5,  6,  7,  8],
        [ 9, 10, 11, 12]])
max, dim=1:
tensor([[ 9, 10, 11, 12],
        [ 9, 10, 11, 12]])
max, dim=2:
tensor([[ 4,  8, 12],
        [12,  4,  8]])
max, dim=-1:
tensor([[ 4,  8, 12],
        [12,  4,  8]])
max, dim=-2:
tensor([[ 9, 10, 11, 12],
        [ 9, 10, 11, 12]])
max, dim=-3:
tensor([[ 9, 10, 11, 12],
        [ 5,  6,  7,  8],
        [ 9, 10, 11, 12]])
```

