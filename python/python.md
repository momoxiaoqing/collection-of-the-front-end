#### 对象
1、strings, tuples, 和 numbers 是不可更改的对象，而 list,dict 等则是可以修改的对象



2、多个变量赋值：
```
a = b = c = 1
a, b, c = 1, 2, "john"
```

#### 基本数据类型
* Numbers（数字）
* String（字符串）
* List（列表）
* Tuple（元组） // 用 () 标识，不能二次赋值，相当于只读列表。
* Dictionary（字典） // 和object差不多

#### 运算符
* 逻辑运算符：and / or / not
* 成员运算符： in / not in
* 身份运算符：is / is not  //判断两个标识符是不是引用自一个对象


#### 循环
* pass:占位置，比如定义空函数的时候需要pass填充，python2.x必须要，python3.x可不写
* while … else： 在循环条件为 false 时执行 else 语句块
* for … else： else 中的语句会在循环正常执行完（即 for 不是通过 break 跳出而中断的）的情况下执行，while … else 也是一样
* for … in：

for遍历带下标
```
fruits = ['banana', 'apple',  'mango']
for index in range(len(fruits)):
   print '当前水果 :', fruits[index]
```
```
fruits = ['banana', 'apple',  'mango']
for index,item in enumerate(fruits):
   print '当前水果 :', item
```

#### 函数
1、命令行直接调用函数，file为Python文件： `python -c 'import file; file.f1()'`
 
2、传参要注意参数是否可变类型：可变类型修改后，fun外部的变量也会受影响

3、参数传递：
* 必备参数
* 关键字参数
* 默认参数
* 不定长参数
```
def printinfo( name, age ):
   "打印任何传入的字符串"
   print("Name: "+name)
   print("Age: %d" % age)
   return

printinfo( "miki" , 40)  # 必备参数
printinfo( age=50, name="miki" )  # 关键字参数

# 默认参数
def printinfo( name, age = 35 ):
    return
```
不定长参数: `def functionname([formal_args,] *var_args_tuple )`
```
def printinfo( arg1, *vartuple ):
   "打印任何传入的参数"
   print "输出: "
   print arg1
   for var in vartuple:
      print var
   return
 
# 调用printinfo 函数
printinfo( 10 )
printinfo( 70, 60, 50 )
```

4、匿名函数：lambda 
语法：`lambda [arg1 [,arg2,.....argn]]:expression`

* lambda只是一个表达式，函数体比def简单很多。
* lambda的主体是一个表达式，而不是一个代码块。仅仅能在lambda表达式中封装有限的逻辑进去。
* lambda函数拥有自己的命名空间，且不能访问自有参数列表之外或全局命名空间里的参数。
* 虽然lambda函数看起来只能写一行，却不等同于C或C++的内联函数，后者的目的是调用小函数时不占用栈内存从而增加运行效率。

#### 模块
模块：
* os // 文件及目录
* file // 文件，不用导入
* math // 数学运算
* cmath // 复数
* re // 正则

函数：
* dir()：返回的列表容纳了在一个模块里定义的所有模块，变量和函数
* globals()：全局名字
* locals()
* reload()：重新执行模块里顶层部分的代码
```
import math

content = dir(math)

print content;
```

#### 异常
```
try:
<语句>        #运行别的代码
except <名字>：
<语句>        #如果在try部份引发了'name'异常
except <名字>，<数据>:
<语句>        #如果引发了'name'异常，获得附加的数据
else:
<语句>        #如果没有异常发生
```

#### 类
* 私有属性和私有方法用2个‘_’开头：__private_attrs、__private_method
* 继承：`class Child(Parent):`

#### 单下划线、双下划线、头尾双下划线说明
* __foo__: 定义的是特殊方法，一般是系统定义名字 ，类似 __init__() 之类的。
* _foo: 以单下划线开头的表示的是 protected 类型的变量，即保护类型只能允许其本身与子类进行访问，不能用于 from module import *
* __foo: 双下划线的表示的是私有类型(private)的变量, 只能是允许这个类本身进行访问了。
