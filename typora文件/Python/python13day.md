# 昨日回顾

+ 生成器：生成器就是迭代器，生成器是自己用python代码构建的
  + 1. 生成器函数
    2. 生成器表达式
    3. python内部提供的
  + 如何判断函数和生成器函数
    + yield
    + yield return
  + 吃包子的区别。
  + yield from将一个可迭代对象，变成一个生成器。
  + 列表推导式、生成器表达式。
    + 循环模式[变量（加工后的变量）for 变量 initerable]
    + 筛选模式[变量（加工后的变量）for 变量 initerable if..]
  + 内置函数。

# 今日内容

+ 如何学习？

  + 一定要预习预习
  + 分配比例

+ 匿名函数lambda

  + ```python
    #匿名函数：一句话函数，比较简单的函数。
    
    #构建普通函数
    def func(a,b):
        return a+b
    #构建匿名函数
    lambda a,b:a+b
    #关键字 形参：返回值（可赋给一个变量）
    ```

    + 多复杂都一行
    + 一般结合内置函数用

+ 内置函数II

+ 闭包：封闭的东西、保证数据安全。

  + 全局变量万一失误被改变，数据不安全

  + 为了数据安全，不能设定为全局变量

  + 但放在局部，每次又会被清空

  + 方案：闭包

    + ```python
      #封闭的东西：保证数据的安全。
      def make_averager():
          l1=[]
          def averager(new_value):
              l1.append(new_value)
              total=sum(l1)
              return total/len(l1)
          return averager
      avg=make_averager()
      print(avg(100000))
      print(avg(110000))
      print(avg(120000))
      print(avg(90000))
      ```

      ![image-20200623115749973](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200623115749973.png)

      闭包只能存在嵌套函数中，内层函数对外层函数非全局变量引用，这个变量被称为自由变量，这个变量会和内层函数产生绑定关系，而且在内存中不会消失

      + 闭包一定有自由变量

        ```python
        #代码判断闭包，有无自由变量
        print(avg.__code__.co_freevars) #('l1',) 
        ```

# 今日总结

1. 匿名函数lambda
2. 内置函数II
3. 闭包

# 明日学习

装饰器

## 代码总行数1887+64=1951行