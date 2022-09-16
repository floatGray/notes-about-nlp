# AI中的python

## 第一章 序言

- 环境配置

Anaconda中的jupyter notebook

Anaconda可以管理库，很方便

- 介绍



## 第二章

python的基本语法，有编程基础基本可以跳过，难度等于伪代码，通俗易懂

- `eval()`函数用来执行一个字符串表达式，并返回表达式的值。

- 格式化输出方式

  ```python
  print("PI = {0},E = {1}".format(PI, E))
  # PI = 3.1415926,E = 2.71828
  print("PI = {1},E = {0}".format(PI, E))
  # PI = 2.71828,E = 3.1415926
  ```

- 修饰输出

  ```python
  print("{0:_^20}".format(PI))
  # _____3.1415926______
  # <^> 左对齐、居中、右对齐、数字代表整个字符串的长度
  ```


## 第三章

python中的数据类型

- 小数不确定问题

  ```python
  0.1+0.2
  # 0.30000000000000004
  ```

- 字符串的切片

  变量名[开始位置：结束位置：切片间隔]

## 第四章

Python中的列表、元组、字典、集合

- 对列表的操作：增删改查排序复制、列表元素的表示

  ```python
  sorted()
  #临时排序，不影响原列表
  ```

  

- 元组是不可写的列表

  ```python
  zip()# 打包两个列表
  ```

- 字典存储的是键值对、无序，其中键要是不可变的
  - 不可变类型：数字、字符串、元组。 &ensp;一旦确定，它自己就是它自己，变了就不是它了。
  - 可变类型：列表、字典、集合。&ensp; 一旦确定，还可以随意增删改。

## 第五章

Python中程序的控制结构，选择循环

- 如果for 循环全部执行完毕，没有被break中止，则运行else块
- 如果while 循环全部执行完毕，没有被break中止，则运行else块

## 第六章

Python中的函数

- **位置参数**，严格按照位置顺序，用实参对形参进行赋值(关联），一般用在参数比较少的时候，实参与形参个数必须一一对应，一个不能多，一个不能少

  ```python
  def function(x, y, z):
      print(x, y, z)
      
      
  function(1, 2, 3)    # x = 1; y = 2; z = 3
  ```

- **关键字参数**,打破位置限制，直呼其名的进行值的传递（形参=实参）,必须遵守实参与形参数量上一一对应

  ```python
  def function(x, y, z):
      print(x, y, z)
      
      
  function(y=1, z=2, x=3)    # x = 3; y = 1; z = 2
  ```

- **默认参数**,在定义阶段就给形参赋值——该形参的常用值,默认参数必须放在非默认参数后面,调用函数时，可以不对该形参传值,默认参数应该设置为不可变类型（数字、字符串、元组）

  ```python
  def register(name, age, sex="male"):
      print(name, age, sex)
  
  register("大杰仔", 18)
  register("林志玲", 38, "female")
  ```

- `*args`接受实参，`**kwargs`接受指定变量名的参数，都可以打散

- 可以有多个return 语句，一旦其中一个执行，代表了函数运行的结束

- 函数式编程

  ```python
  import random
  
  
  def get_inputs():  
      # 输入原始数据
      prob_A = eval(input("请输入运动员A的每球获胜概率(0~1)："))
      prob_B = round(1-prob_A, 2)
      number_of_games = eval(input("请输入模拟的场次（正整数）："))
      print("模拟比赛总次数：", number_of_games)
      print("A 选手每球获胜概率：", prob_A)
      print("B 选手每球获胜概率：", prob_B)
      return prob_A, prob_B, number_of_games
  
  
  def game_over(score_A, score_B):
      # 单场模拟结束条件，一方先达到21分，比赛结束    
      return score_A == 21 or score_B == 21
  
  
  def sim_one_game(prob_A, prob_B):
      # 模拟一场比赛的结果
      score_A, score_B = 0, 0
      while not game_over(score_A, score_B):
          if random.random() < prob_A:                # random.random() 生产[0,1)之间的随机小数,均匀分布
              score_A += 1                 
          else:
              score_B += 1
      return score_A, score_B
  
  
  def sim_n_games(prob_A, prob_B, number_of_games):
      # 模拟多场比赛的结果
      win_A, win_B = 0, 0                # 初始化A、B获胜的场次
      for i in range(number_of_games):   # 迭代number_of_games次
          score_A, score_B = sim_one_game(prob_A, prob_B)  # 获得模拟依次比赛的比分
          if score_A > score_B:
              win_A += 1
          else:
              win_B += 1
      return win_A, win_B
  
  
  def print_summary(win_A, win_B, number_of_games):
      # 结果汇总输出
      print("共模拟了{}场比赛".format(number_of_games))
      print("\033[31m选手A获胜{0}场，占比{1:.1%}".format(win_A, win_A/number_of_games))
      print("选手B获胜{0}场，占比{1:.1%}".format(win_B, win_B/number_of_games))
      
  
  def main():
      # 主要逻辑
      prob_A, prob_B, number_of_games = get_inputs()                        # 获取原始数据
      win_A, win_B = sim_n_games(prob_A, prob_B, number_of_games)           # 获取模拟结果
      print_summary(win_A, win_B, number_of_games)                          # 结果汇总输出
  
  
  if __name__ == "__main__":
      main()
  ```

- 匿名函数，使用方式`key = lambda x: x[0]+x[1]`

  ```python
  ls = [(93, 88), (79, 100), (86, 71), (85, 85), (76, 94)]
  temp = sorted(ls, key = lambda x: x[0]+x[1], reverse=True)
  ```

- 面向对象的思考方式

## 第七章

Python中的类

- 类的定义
- 创建实例
- 类的继承
- 重写

## 第八章

Python中文件的读取、异常和模块

- `*with* open("文件路径", "打开模式", *encoding* = "操作文件的字符编码") *as* f:`

- **打开模式缺省，默认为只读模式**

- 逐行进行读取——`f.readline()`

- 读入所有行，以每行为元素形成一个列表——`f.readlines()`

- ```python
  with open("三国演义片头曲_gbk.txt", "r", encoding="gbk") as f:     
      for text in f:         # f本身就是一个可迭代对象，每次迭代读取一行内容 
          print(text)  
  ```

- 向文件写入一个字符串或字节流（二进制）——`f.write()`

- 将一个元素为字符串的列表整体写入文件——`f.writelines()`

- ```python
  with open("浪淘沙_北戴河.txt", "r+", encoding="gbk") as f:
  #     for line in f:
  #         print(line)   # 全部读一遍后，指针到达结尾
      f.seek(0,2)         # 或者可以将指针移到末尾f.seek(偏移字节数,位置（0：开始；1：当前位置；2：结尾）)
      text = ["萧瑟秋风今又是，\n", "换了人间。\n"]
      f.writelines(text)
  ```

- csv是由逗号将数据分开的字符序列，可以由excel打开和json常被用来存储字典类型

- 异常处理

  - 除0运算——ZeroDivisionError
  - 找不到可读文件——FileNotFoundError
  - 值错误——ValueError
  - 索引错误——IndexError
  - 类型错误——TypeError
  - NameError 使用一个未被定义的变量  
  - KeyError 试图访问字典里不存在的键 

- try_except。如果try内代码块顺利执行，except不被触发如果try内代码块发生错误，触发except,执行except内代码块

- 万能异常 Exception （所有错误的老祖宗）

- try_except_else：如果try 模块执行，则else模块也执行，可以将else 看做try成功的额外奖赏

- try_except_finally：不论try模块是否执行，finally最后都执行

- 模块：已经被封装好  无需自己再“造轮子”  声明导入后，拿来即用

- 时间库time &ensp;随机库random 容器数据类型collection\ &ensp;迭代器函数itertools&emsp;数据分析numpy、pandas\ &ensp;数据可视化matplotlib\ &ensp;机器学习scikit-learn\ &ensp;深度学习Tensorflow

- 导入模块中所有的类和函数**——from 模块 import *

  ```python
  from random import * 
  
  print(randint(1,100))       # 产生一个[1,100]之间的随机整数
  print(random())             # 产生一个[0,1)之间的随机小数
  ```

  

## 第九章

python的细节

- 浅拷贝就是多一个指针指向地址

- **引用数组的概念**  列表内的元素可以分散的存储在内存中  列表存储的，实际上是这些**元素的地址！地址的存储在内存中是连续的

- 修改列表原来的元素会改变浅拷贝的列表的值，新增一个全新的值则不会改变浅拷贝的值

- 对元组型元素进行操作，由于是元组不可变，所以实际上是生成了一个新地址指向新元组

- **浅拷贝之后**  针对不可变元素（数字、字符串、元组）的操作，都各自生效了  针对不可变元素（列表、集合）的操作，发生了一些混淆

- 深拷贝：深拷贝将所有层级的相关元素全部复制，完全分开，泾渭分明，避免了上述问题

- 字典字典数据类型，通过空间换时间，实现了快速的数据查找因为散列值对应位置的顺序与键在字典中显示的顺序可能不同，因此表现出来字典是无序的

- **通过紧凑数组实现字符串的存储**

- ```python
  ls = [[0]*10]*5 # 这个是把一个列表浅拷贝了5份
  ```

- 解析语法[expression **for value in iterable** if conditihon]三要素：表达式、可迭代对象、if条件（可选）

- 条件表达式

- 三大神器

- **生成器** 1）采用惰性计算的方式  2）无需一次性存储海量数据  3）一边执行一边计算，只计算每次需要的值4）实际上一直在执行next()操作，直到无值可取

- 生成器函数——yield

- 可以被next()函数调用并不断返回下一个值，直至没有数据可取的对象称为迭代器：Iterator

- **闭包：延伸了作用域的函数**  

  **如果一个函数定义在另一个函数的作用域内，并且引用了外层函数的变量，则该函数称为闭包**

  **闭包是由函数及其相关的引用环境组合而成的实体(即：闭包=函数+引用环境)**

- 装饰器

  ```python
  import time
  
  
  def timer(func):
      
      def inner(*args, **kwargs):
          print("inner run")
          start = time.time()
          func(*args, **kwargs)
          end = time.time()
          print("{} 函数运行用时{:.2f}秒".format(func.__name__, (end-start)))
      
      return inner
  
  
  @timer                # 相当于实现了f1 = timer(f1)
  def f1(n):
      print("f1 run")
      time.sleep(n)
  
      
  f1(2)
  ```

  

# 第十章

Python中的标准库

- time

  `time.time()` `time.perf_counter()` `time.process_time()` `time.strftime`

  ```python
  lctime = time.localtime()
  time.strftime("%Y-%m-%d %A %H:%M:%S", lctime)
  # '2022-09-15 Thursday 10:04:58'
  ```

- random

  相同种子会产生相同的随机数,如果不设置随机种子，以系统当前时间为默认值

  `choice(seq)`从序列类型中随机返回一个元素

  `choices(seq,weights=None, k)`对序列类型进行k次重复采样，可设置权重

  `choices(['win', 'lose', 'draw'], [4,4,2], *k*=10)`

- collections

  namedtuple——具名元组\Counter——计数器工具\deque——双向队列

- itertools库——迭代器

  product——笛卡尔积\permutations——排列\combinations——组合\zip——短拉链\zip_longest——长拉链

  itertools 其他函数可参考官方文档

## 第十一章

Numpy

- 在数据处理的过程中，遇到使用“Python for循环” 实现一些向量化、矩阵化操作的时候，要优先考虑用Numpy

## 第十二章

Pandas

- 基于Numpy构建的Pandas库，提供了使得数据分析变得更快更简单的高级数据结构和操作工具
- 通用结构: pd.Series(data, index=index, dtype=dtype)
- data：数据，可以是列表，字典或Numpy数
- index：索引，为可选参数
- dtype: 数据类型，为可选参数


## 第十三章


## 第十四章

## 第十五章