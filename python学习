# 编程语言（Python）

---

# 目录

| Chapter 1 | Chapter 2 | Chapter 3 | 
| :---------: | :---------: | :---------: | 
| [编程基础](#base)|[数据结构](#datastruct)|[面向对象](#oop)|

---

# 内容

### <span id = "base">编程基础</span>

由于之前在学习看过一点python的语法，因此这一次主要记录一下之前不熟悉的地方，以供之后复习之需。
主要参考了《简明Python教程（4th）》以及《菜鸟教程》.

## 控制流

 1. break语句:
 
     - break语句用以中断(Break)循环语句,也就是中止循环语句的执行,即使循环条件没有变更为False,
或队列中的项目尚未完全迭代依旧如此。

     - 有一点需要尤其注意,如果你中断了一个for或while循环,任何相应循环中的else块都将不会被执行。
     
 2. contiune语句：
     - continue用以告诉Python跳过当前循环块中的剩余语句,并继续该循环的下一次迭代。

## 函数：

1. 可变参数
    - 有时你可能想定义的函数里面能够有任意数量的变量,也就是参数数量是可变的,这可以通过使用星号来实现.

实例：

	def total(a=5,*numbers,**phonebook):
		print('a',a)	
	遍历元组中的所有项目
	        for single_item in numbers:
			print('single_item',single_item)
	遍历字典中的所有项目
	        for first_part,second_part in phonebook.items():
		        print(first_part,second_part)
	print(total(10,1,2,3,Jack=1123,John=2231,Inge=1560))

输出:

	$	python	function_varargs.py
	a	10
	single_item	1
	single_item	2
	single_item	3
	Inge	1560
	John	2231
	Jack	1123
	None
	
    - 它是如何工作的当我们声明一个诸如*param的星号参数时,从此处开始直到结束的所有位置参数(Positional Arguments)都将被收集并汇集成一个称为“param”的元组(Tuple)。类似地,当我们声明一个诸如\**param的双星号参数时,从此处开始直至结束的所有关键字参数都将被收集并汇集成一个名为	 param的字典(Dictionary)。

## 模块：

    - 编写模块有很多种方法,其中最简单的一种便是创建一个包含函数与变量、以.py为后缀的文件。
    - 另一种方法是使用撰写Python解释器本身的本地语言来编写模块。举例来说,你可以使用C语言来撰写Python模块,并且在编译后,你可以通过标准Python解释器在你的Python代码中使用它们。

    - 如果它不是一个已编译好的模块,即用Python	编写的模块,那么Python解释器将从它的sys.path变量所提供的目录中进行搜索。如果找到了对应模块,则该模块中的语句将在开始运行,并能够为你所使用。  注意：所以如果出现找不到模块的错误，要想到环境变量设置了吗？

1. import:
    - import sys
    
    通过sys.来使用sys里面的功能比如：sys.argv

2. from..import语句：
    - 如果你希望直接将argv变量导入你的程序(为了避免每次都要输入sys.),那么你可以通过使用from sys import argv 语句来实现这一点。

3. 模块的 __name__
    - 每个模块都有一个名称,而模块中的语句可以找到它们所处的模块的名称。这对于确定模块是独立运行的还是被导入进来运行的这一特定目的来说大为有用。当模块第一次被导入时,它所包含的代码将被执行。我们可以通过这一特性来使模块以不同的方式运行,这取决于它是为自己所用还是从其它从的模块中导入而来。这可以通过使用模块的__name__属性来实现。

案例(保存为module_using_name.py):
    
	if __name__=='__main__':
		print('This program	is	being	run	by	itself')
	else:
		print('I am being imported from	another	module')
输出:

	$ python module_using_name.py
	This program is being run by itself
	$ python
	>>>import module_using_name 
	I am being imported from another module

    - 它是如何工作的
    每一个Python模块都定义了它的__name__属性。如果它与__main__属性相同则代表这一模块是由用户独立运行的,因此我们便可以采取适当的行动。

4. dir函数：
    - 内置的dir()函数能够返回由对象所定义的名称列表。如果这一对象是一个模块,则该列表会包括函数内所定义的函数、类与变量。该函数接受参数。如果参数是模块名称,函数将返回这一指定模块的名称列表。如果没有提供参数,函数将返回当前模块的名称列表。


## 包

1. 包是指一个包含模块与一个特殊的__init__.py文件的文件夹,后者向Python表明这一文件夹是特别的,因为其包含了Python模块。
    - 让我们这样设想:你想创建一个名为“world”的包,其中还包含着“asia”、“africa”等其它子包,同时这些子包都包含了诸如“india”、“madagascar”等模块。

下面是你会构建出的文件夹的结构:
	-<some	folder	present	in	the	sys.path>/
	-world/
		-__init__.py
		-asia/
			-__init__.py
			-india/													                       -__init__.py													       -foo.py
		-africa/
	                -__init__.py
		        -madagascar/													               -__init__.py												               -bar.py
    包是一种能够方便地分层组织模块的方式。


### <span id = "datastruct">数据结构</span>

# python字符串：

Python访问字符串中的值：
Python不支持单字符类型，单字符在 Python 中也是作为一个字符串使用。

Python访问子字符串，可以使用方括号来截取字符串，如下实例：

实例(Python 2.0+)
#!/usr/bin/python
 
var1 = 'Hello World!'
var2 = "Python Runoob"
 
print "var1[0]: ", var1[0]
print "var2[1:5]: ", var2[1:5]
以上实例执行结果：

var1[0]:  H
var2[1:5]:  ytho

#python字符串更新


 
var1 = 'Hello World!'
 
print "更新字符串 :- ", var1[:6] + 'Runoob!'

执行结果：更新字符串 :-  Hello Runoob!



#Python字符串运算符
+	字符串连接	
>>>a + b
'HelloPython'

*	重复输出字符串	
>>>a * 2
'HelloHello'

[]	通过索引获取字符串中字符	
>>>a[1]
'e'

[ : ]	截取字符串中的一部分	
>>>a[1:4]
'ell'

in	成员运算符 - 如果字符串中包含给定的字符返回 True	
>>>"H" in a
True

not in	成员运算符 - 如果字符串中不包含给定的字符返回 True	
>>>"M" not in a
True




# Python列表
list[0] ：访问列表list的第一个
append:在列表后增加
del:删除

Python列表脚本操作符：列表对 + 和 * 的操作符与字符串相似。+ 号用于组合列表，* 号用于重复列表

Python列表函数&方法：






# Python元组

Python的元组与列表类似，不同之处在于元组的元素不能修改。

元组使用小括号，列表使用方括号。

元组创建很简单，只需要在括号中添加元素，并使用逗号隔开即可


1.访问（与列表相似）
tup1 = ('physics', 'chemistry', 1997, 2000)

print "tup1[0]: ", tup1[0]

输出：tup1[0]:  physics

2.修改元组：元组中的元素值是不允许修改的，但我们可以对元组进行连接组合，如下实例:

tup1 = (12, 34.56)
tup2 = ('abc', 'xyz')
 
# 以下修改元组元素操作是非法的。
# tup1[0] = 100
 
# 创建一个新的元组
tup3 = tup1 + tup2
print tup3

以上实例输出结果：

(12, 34.56, 'abc', 'xyz')

3.删除元组：
元组中的元素值是不允许删除的，但我们可以使用del语句来删除整个元组，如下实例:

实例(Python 2.0+)：
#!/usr/bin/python
 
tup = ('physics', 'chemistry', 1997, 2000)
 
print tup
del tup
print "After deleting tup : "
print tup

输出如下所示：

('physics', 'chemistry', 1997, 2000)
After deleting tup :
Traceback (most recent call last):
  File "test.py", line 9, in <module>
    print tup
NameError: name 'tup' is not defined



注意：任意无符号的对象，以逗号隔开，默认为元组，如下实例：
print 'abc', -4.24e93, 18+6.6j, 'xyz'
x, y = 1, 2
print "Value of x , y : ", x,y
运行结果：
abc -4.24e+93 (18+6.6j) xyz
Value of x , y : 1 2




# Python字典
字典是另一种可变容器模型，且可存储任意类型对象。

字典的每个键值 key=>value 对用冒号 : 分割，每个键值对之间用逗号 , 分割，整个字典包括在花括号 {} 中 ,格式如下所示：

d = {key1 : value1, key2 : value2 }

键一般是唯一的，如果重复最后的一个键值对会替换前面的，值不需要唯一。

>>>dict = {'a': 1, 'b': 2, 'b': '3'}
>>> dict['b']
'3'
>>> dict
{'a': 1, 'b': '3'}

值可以取任何数据类型，但键必须是不可变的，如字符串，数字或元组。

1.访问字典里的值：

dict = {'Name': 'Zara', 'Age': 7, 'Class': 'First'}
 
print "dict['Name']: ", dict['Name']
输出：dict['Name']:  Zara

2.修改字典
实例：
dict = {'Name': 'Zara', 'Age': 7, 'Class': 'First'}
 
dict['Age'] = 8 # 更新
dict['School'] = "RUNOOB" # 添加
 
 
print "dict['Age']: ", dict['Age']
print "dict['School']: ", dict['School']

输出：
dict['Age']:  8
dict['School']:  RUNOOB

3.删除字典元素
dict = {'Name': 'Zara', 'Age': 7, 'Class': 'First'}
 
del dict['Name']  # 删除键是'Name'的条目
dict.clear()      # 清空词典所有条目
del dict          # 删除词典


print "dict['Age']: ", dict['Age'] 
print "dict['School']: ", dict['School']

输出：
dict['Age']:
Traceback (most recent call last):
  File "test.py", line 8, in <module>
    print "dict['Age']: ", dict['Age'] 
TypeError: 'type' object is unsubscriptable


4.字典键的特性：
字典值可以没有限制地取任何python对象，既可以是标准的对象，也可以是用户定义的，但键不行。

两个重要的点需要记住：

1）不允许同一个键出现两次。创建时如果同一个键被赋值两次，后一个值会被记住。
2）键必须不可变，所以可以用数字，字符串或元组充当，所以用列表就不行，实例如下：
dict = {['Name']: 'Zara', 'Age': 7} 
 
print "dict['Name']: ", dict['Name']

输出：
Traceback (most recent call last):
  File "test.py", line 3, in <module>
    dict = {['Name']: 'Zara', 'Age': 7} 
TypeError: list objects are unhashable


5.字典内置函数&方法





### <span id = "oop">面向对象</span>

# 创建类
 
使用 class 语句来创建一个新类，class 之后为类的名称并以冒号结尾:

class ClassName:
   '类的帮助信息'   #类文档字符串
   class_suite  #类体

实例：
class Employee:
   '所有员工的基类'
   empCount = 0
 
   def __init__(self, name, salary):
      self.name = name
      self.salary = salary
      Employee.empCount += 1
   
   def displayCount(self):
     print "Total Employee %d" % Employee.empCount
 
   def displayEmployee(self):
      print "Name : ", self.name,  ", Salary: ", self.salary

     注意：其中，（1）empCount 变量是一个类变量，它的值将在这个类的所有实例之间共享。你可以在内部类或外部类使用 Employee.empCount 访问。

        （2）第一种方法__init__()方法是一种特殊的方法，被称为类的构造函数或初始化方法，当创建了这个类的实例时就会调用该方法

        （3）self 代表类的实例，self 在定义类的方法时是必须有的，虽然在调用时不必传入相应的参数。

self代表类的实例，而非类：类的方法与普通的函数只有一个特别的区别——它们必须有一个额外的第一个参数名称, 按照惯例它的名称是 self。
实例：
  class Test:
    def prt(self):
        print(self)
        print(self.__class__)
 
  t = Test()
  t.prt()

输出为：<__main__.Test instance at 0x10d066878>
        __main__.Test

从执行结果可以很明显的看出，self 代表的是类的实例，代表当前对象的地址，而 self.__class__ 则指向类。

self 不是 python 关键字，我们把他换成字母也是可以正常执行的:


2.创建实例对象：
    实例化类其他编程语言中一般用关键字 new，但是在 Python 中并没有这个关键字，类的实例化类似函数调用方式。以下使用类的名称 Employee 来实例化，并通过 __init__ 方法接收参数。

   实例：
        "创建 Employee 类的第一个对象"
        emp1 = Employee("Zara", 2000)
        "创建 Employee 类的第二个对象"
        emp2 = Employee("Manni", 5000)
             
3.访问属性：
  您可以使用点号 . 来访问对象的属性。使用如下类的名称访问类变量:
   


        emp1.displayEmployee()
        emp2.displayEmployee()
        print "Total Employee %d" % Employee.empCount

完整实例如下：
#!/usr/bin/python
# -*- coding: UTF-8 -*-
 
        class Employee:
           '所有员工的基类'
           empCount = 0
         
           def __init__(self, name, salary):
              self.name = name
              self.salary = salary
              Employee.empCount += 1
           
           def displayCount(self):
             print "Total Employee %d" % Employee.empCount
         
           def displayEmployee(self):
              print "Name : ", self.name,  ", Salary: ", self.salary
         
        "创建 Employee 类的第一个对象"
        emp1 = Employee("Zara", 2000)
        "创建 Employee 类的第二个对象"
        emp2 = Employee("Manni", 5000)
        emp1.displayEmployee()
        emp2.displayEmployee()
        print "Total Employee %d" % Employee.empCoun

你可以添加，删除，修改类的属性，如下所示：
        emp1.age = 7  # 添加一个 'age' 属性
        emp1.age = 8  # 修改 'age' 属性
        del emp1.age  # 删除 'age' 属性
        你也可以使用以下函数的方式来访问属性：

        getattr(obj, name[, default]) : 访问对象的属性。
        hasattr(obj,name) : 检查是否存在一个属性。
        setattr(obj,name,value) : 设置一个属性。如果属性不存在，会创建一个新属性。
        delattr(obj, name) : 删除属性。
        hasattr(emp1, 'age')    # 如果存在 'age' 属性返回 True。
        getattr(emp1, 'age')    # 返回 'age' 属性的值
        setattr(emp1, 'age', 8) # 添加属性 'age' 值为 8
        delattr(emp1, 'age')    # 删除属性 'age'


4.python内置类属性：
    __dict__ : 类的属性（包含一个字典，由类的数据属性组成）
    __doc__ :类的文档字符串
    __name__: 类名
    __module__: 类定义所在的模块（类的全名是'__main__.className'，如果类位于一个导入模块mymod中，那么 className.__module__ 等于 mymod）
    __bases__ : 类的所有父类构成元素（包含了一个由所有父类组成的元组）


       

# Python对象销毁






# 类的继承

1.继承的语法：class 派生类名(基类名)

2.在python中继承中的一些特点：

1、如果在子类中需要父类的构造方法就需要显示的调用父类的构造方法，或者不重写父类的构造方法。详细说明可查看：python 子类继承父类构造函数说明。
2、在调用基类的方法时，需要加上基类的类名前缀，且需要带上 self 参数变量。区别在于类中调用普通函数时并不需要带上 self 参数
3、Python 总是首先查找对应类型的方法，如果它不能在派生类中找到对应的方法，它才开始到基类中逐个查找。（先在本类中查找调用的方法，找不到才去基类中找）。
3.如果在继承元组中列了一个以上的类，那么它就被称作"多重继承" 。

3.多重继承语法：

派生类的声明，与他们的父类类似，继承的基类列表跟在类名之后，如下所示：

class SubClassName (ParentClass1[, ParentClass2, ...]):






你可以使用issubclass()或者isinstance()方法来检测。

issubclass() - 布尔函数判断一个类是另一个类的子类或者子孙类，语法：issubclass(sub,sup)
isinstance(obj, Class) 布尔函数如果obj是Class类的实例对象或者是一个Class子类的实例对象则返回true。



4.方法重写


如果你的父类方法的功能不能满足你的需求，你可以在子类重写你父类的方法：

实例：

#!/usr/bin/python
# -*- coding: UTF-8 -*-
 
class Parent:        # 定义父类
   def myMethod(self):
      print '调用父类方法'
 
class Child(Parent): # 定义子类
   def myMethod(self):
      print '调用子类方法'
 
c = Child()          # 子类实例
c.myMethod()         # 子类调用重写方法

执行结果：
调用子类方法


5.基础重载方法

6.运算符重载
    实例如下：#!/usr/bin/python
 
        class Vector:
           def __init__(self, a, b):
              self.a = a
              self.b = b
         
           def __str__(self):
              return 'Vector (%d, %d)' % (self.a, self.b)
           
           def __add__(self,other):
              return Vector(self.a + other.a, self.b + other.b)
         
        v1 = Vector(2,10)
        v2 = Vector(5,-2)
        print v1 + v2



7.类的私有方法：
  类属性与方法
  类的私有属性
  __private_attrs：两个下划线开头，声明该属性为私有，不能在类的外部被使用或直接访问。在类内部的方法中使用时 self.__private_attrs。

类的方法
  在类的内部，使用 def 关键字可以为类定义一个方法，与一般函数定义不同，类方法必须包含参数 self,且为第一个参数

类的私有方法
  __private_method：两个下划线开头，声明该方法为私有方法，不能在类的外部调用。在类的内部调用 self.__private_methods

实例
#!/usr/bin/python
# -*- coding: UTF-8 -*-
 
class JustCounter:
    __secretCount = 0  # 私有变量
    publicCount = 0    # 公开变量
 
    def count(self):
        self.__secretCount += 1
        self.publicCount += 1
        print self.__secretCount
 
counter = JustCounter()
counter.count()
counter.count()
print counter.publicCount
print counter.__secretCount  # 报错，实例不能访问私有变量

输出：
Traceback (most recent call last):
  File "test.py", line 17, in <module>
    print counter.__secretCount  # 报错，实例不能访问私有变量
AttributeError: JustCounter instance has no attribute '__secretCount'

Python不允许实例化的类访问私有数据，但你可以使用 object._className__attrName（ 对象名._类名__私有属性名 ）访问属性，参考以下实例：

#!/usr/bin/python
# -*- coding: UTF-8 -*-

class Runoob:
    __site = "www.runoob.com"

runoob = Runoob()
print runoob._Runoob__site
执行以上代码，执行结果如下：

www.runoob.com




