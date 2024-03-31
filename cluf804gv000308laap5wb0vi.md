---
title: "Fintech"
datePublished: Sun Mar 31 2024 07:49:11 GMT+0000 (Coordinated Universal Time)
cuid: cluf804gv000308laap5wb0vi
slug: fintech
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/W7wEqy01K3s/upload/1fdac6af435ce44186d42621e805970c.jpeg
tags: python, learning, fintech, thinking

---

# Python

Because i have learnt Python in 1 year before, I don't want to learn it from totally 'zero'. I would record some knowledge points that I have forgotten in Python.

## Fundamental knowledge in Python

### Copy

```python
my_list = [1.1, 2.2, 3.3]
my_copy = my_list
print(my_copy)

my_copy[0] = 10

print(my_copy)
print(my_list)
```

```python
[1.1, 2.2, 3.3]
[10, 2.2, 3.3]
[10, 2.2, 3.3]
```

从上面的代码以及输出可以看出，当我们对一个list进行复制拷贝后，新命名的列表占用的内存和原来的列表是一样的，这类似于C++中的引用，所以如果我们想生成一个新的列表，列表的内容和目标复制的列表内容一样，我们就需要使用深拷贝。

注意需要先导入模块‘copy’。

```python
import copy
my_list = [1.1, 2.2, 3.3]

my_copy = copy.deepcopy(my_list)
my_copy[0] = 10

print(my_copy)
print(my_list)

#output：
[10, 2.2, 3.3]
[1.1, 2.2, 3.3]
```

### Loop

关于enumerate，这个函数可以自动将你的列表里的数据加上顺序index，即枚举

```python
for (index,element) in enumerate(myList):
    print("Element",index,"in list is:",element)
    
print("-------")
```

```python
Element 0 in list is: hello
Element 1 in list is: 1
Element 2 in list is: True
Element 3 in list is: 1000
-------
```

### Dictionary

```python
stock_op__dic = {'AAPL': 
                     {"underlying":
                     {"open":100.1, "high":102.5, "low": 99.5, "close":101.0},
                     "options":
                     {"strike": 100, "option_type": "Call", "price": 1.5}}, 
                 'MSFT':
                     {"underlying":
                     {"open": 55.5, "high": 65.5,"low": 50.0, "close":52.0},
                     "options":
                     {"strike": 50, "option_type": "Put", "price": 2.5}}} 

for symbol in stock_op__dic.keys():
    print(symbol, stock_op__dic[symbol]["options"]["option_type"],  
          "option with strike", 
          stock_op__dic[symbol]["options"]["strike"],"has price", 
          stock_op__dic[symbol]["options"]["price"])
    
    
```

```python
AAPL Call option with strike 100 has price 1.5
MSFT Put option with strike 50 has price 2.5
```

### Computation time

这里会用到numpy中的linspace函数，此函数通过定义均匀间隔创建数值序列。其实，需要指定间隔起始点、终止端，以及指定分隔值总数（包括起始点和终止点）；最终函数返回间隔类均匀分布的数值序列。

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711700798193/bb189868-97ce-40fc-af79-8d0bb7990ad7.png align="center")

还有python内置的round函数，本质是用来做四舍五入或者设置保留小数位数的。具体的法则可以看链接[round（）函数](https://blog.csdn.net/m0_73419365/article/details/129821610?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522171170081016800185836337%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=171170081016800185836337&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-129821610-null-null.142^v100^pc_search_result_base4&utm_term=round&spm=1018.2226.3001.4187)。

计算时间样例：

```python
def sumInteg_np(n):
    return np.sum(np.linspace(1,n+1, n))

n = 10000000

t0 = time.time()
_sumInteg = sumInteg(n)
t1 = time.time() - t0

t0 = time.time()
_sumInteg_list_comprehension = sumInteg_list_comprehension(n)
t2 = time.time() - t0

t0 = time.time()
_sumInteg_list_comprehension2 = sumInteg_list_comprehension2(n)
t3 = time.time() - t0

t0 = time.time()
_sumInteg_np = sumInteg_np(n)
t4 = time.time() - t0

t0 = time.time()
_sumInteg_Formula = sumInteg_Formula(n)
t5 = time.time() - t0

print("Sum:", sumInteg(n), round(t1, 4))
print("Sum list:", _sumInteg_list_comprehension, round(t2, 4))
print("Sum list 2:", _sumInteg_list_comprehension2, round(t3, 4))
print("Sum numpy:", _sumInteg_np, round(t4, 4))
print("Theoretical:", _sumInteg_Formula, round(t5, 4))
```

```python
Sum: 50000005000000 0.7917
Sum list: 50000005000000 0.9654
Sum list 2: 50000005000000 0.2357
Sum numpy: 50000010000000.08 0.0911
Theoretical: 50000005000000.0 0.0001
```

## Data frames

```python
import numpy as np
import pandas as pd
import matplotlib.pylab as plt
%matplotlib inline
```

前面导入各种库是做分析必要的，而最后的一行%matplotlib inline是干什么的呢？在stack overflow上面查询可以得知，如果我们如果在ipython环境中如果想生成图像，就需要提前写入这句话，具体官方文档解释如下：

> To set this up, before any plotting or import of `matplotlib` is performed you must execute the `%matplotlib magic command`. This performs the necessary behind-the-scenes setup for IPython to work correctly hand in hand with `matplotlib`; it does not, however, actually execute any Python import commands, that is, no names are added to the namespace.
> 
> A particularly interesting backend, provided by IPython, is the `inline` backend. This is available only for the Jupyter Notebook and the Jupyter QtConsole. It can be invoked as follows:
> 
> ```python
> %matplotlib inline
> ```
> 
> With this backend, the output of plotting commands is displayed inline within frontends like the Jupyter notebook, directly below the code cell that produced it. The resulting plots will then also be stored in the notebook document.

关于这三个库各自是干什么的以及具体使用方法细节，在kaggle的网站上给了比较详细的解释，可以点击链接查看 [Numpy,Pandas and Matplotlib](https://www.kaggle.com/code/chats351/introduction-to-numpy-pandas-and-matplotlib) 。