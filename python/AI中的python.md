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

## 第九章

## 第十章

## 第十一章


## 第十二章


## 第十三章


## 第十四章

## 第十五章