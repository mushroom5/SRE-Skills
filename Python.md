# Python
### 数据类型
* 整数
* 浮点数
* 字符串
* 布尔值
* 空值
* 

###  字符串
* title() :以首字母大写的方式显示每个单词
* upper() :全部大写
* lower() :全部小写
* '+' ：拼接
* rstrip() :删除字符串末尾多余的空白
* lstrip() :删除字符串开头多余的空白
* strip() :删除字符串两头多余的空白

### 数字
* 整数：+ — * / （乘方） %（求模运算）
* str() :将非字符串类型值转换成字符串

### 注释
* #
* 目的：代码要做什么 如何做的

### 列表
* 概念：列表由一系列按特定顺序的元素组成。
* 表示：[ ]
* 特点:
    * 1、有序的集合
    * 2、通过偏移来索引，从而读取数据
    * 3、支持嵌套
    * 4、可变的类型
     
-------

修改列表元素：`列表名[索引值] = 新值`

-------

添加列表元素：
		* 在列表末尾添加元素：append()   `列表名.append(需添加的元素)`
		* 在列表中插入元素：insert()        `列表名.insert(索引,需添加的元素)`
		
-------

删除列表元素：
		* 已知要删除的元素在列表中的位置：del        `del 列表名[索引]`    ---删除之后无法访问
		* 删除列表末尾的元素：`pop()`   ---删除之后可保存在变量里继续访问
		* 删除任何列表中的元素：`pop(索引)`
		* 根据值删除元素：`remove()`
		
-------

组织列表：
		* 永久性排序：正序：`sort()`    反序：`sort(reverse=True)`
		* 临时排序：  `sorted()`
		* 倒着打印列表：`reverse()`
		* 确定列表的长度：`len()`
		
-------

遍历列表
		* for 循环    `for item in 列表:`
		
-------

创建数值列表
		* `range()`：生成一系列数字。
    	`range(2,11,2) 从2开始，不断加2，直到达到或超过终值。`
		* `list()`：可是将range()的结果直接转换成列表。
		* `min()`：寻找列表最小值
		* `max()`：寻找列表最大值
		* `sum()`：列表元素和
		
-------

列表解析(列表生成式)：

```
squares = [value**2 for value in range(1,11)]  
print(squares)
```


```
[x * x for x in range(1, 11) if x % 2 == 0]
[4, 16, 36, 64, 100]
```


```
[m + n for m in 'ABC' for n in 'XYZ']
['AX', 'AY', 'AZ', 'BX', 'BY', 'BZ', 'CX', 'CY', 'CZ']
```

-------
生成器：在Python中，一边循环一边计算的机制，称为生成器：generator。
1.创建一个generator方法一：只要把一个列表生成式的`[]`改成`()`

```
>>> g = (x * x for x in range(10))
>>> for n in g:
...     print(n)
... 
0
1
4
9
16
25
36
49
64
81
```
2.创建一个generator方法二：如果一个函数定义中包含`yield`关键字，那么这个函数就不再是一个普通函数，而是一个generator.
斐波那契：

```
def fib(max):
    n, a, b = 0, 0, 1
    while n < max:
        yield b
        a, b = b, a + b
        n = n + 1
    return 'done'
    
>>> for n in fib(6):
...     print(n)
...
1
1
2
3
5
8
```


-------


切片：指定要使用的第一个元素和最后一个元素的索引

```
players = ['charles','martina','micheal','florence','eli']      print(players[1:3])
```

-------

遍历切片：

```
for player in players[:3]:
print(player.title())
```

-------

复制列表: 创建一个包含整个列表的切片，同时省略起始索引和终止索引（[:]）

-------

### 元组
不可变的列表被称为`元组`。
表示: `( )`
虽然不能修改元组的元素，但是可以给存储元组的`变量`赋值。

-------

### IF
条件测试:每条if语句的核心都是一个值为True或False的表达式，这种表达式被称为**条件测试**。
检查是否相等： ==
检查是否不相等：！=
与：and
或：or
检查特定值是否包含在列表中：in
检查特定值是否不包含在列表中：not in
if-elif-else
检查列表是否为空:

```
requested_toppings = []
if requested_toppings:
	for requested_topping in requested_toppings:
		print("Adding" + requested_topping +".")
	print("\nFinished making your pizza")
else:
	 print("Are you sure you want a plain pizza?")
```

-------

###  字典
概念：字典是一系列键值对，每个键都与一个值相关联。
表示：{'key':'value',...}
字典是一种动态结构。
删除键值对：del 字典名['key']
遍历字典：
#### 遍历所有的键-值对

```
遍历所有的键-值对,items()
user_0 = {
	'username':'efermi',
	'first':'enrico',
	'last':'fermi',
    }

for key,value in *user_0.items():*
	print("\nKey: "+ key)
	print("\nValue: " + value)
```
#### 遍历字典中的所有键
```
遍历字典中的所有键，keys()
favorite_languages = {
	'jen':'python',
	'sarah':'C',
	'edward':'ruby',
	'phil':'python',
    }

for name in favorite_languages.keys():
 	print(name.title())
```
#### 按顺序遍历字典中的所有键
```
for循环中对返回的键进行排序，sorted()
favorite_languages = {
	'jen':'python',
	'sarah':'C',
	'edward':'ruby',
	'phil':'python',
    }

for name in sorted(favorite_languages.keys()):
 	print(name.title() + ", thanks you for taking the poll")
```
#### 遍历字典中的所有值
```
遍历字典中的所有值，values()
favorite_languages = {
	'jen':'python',
	'sarah':'C',
	'edward':'ruby',
	'phil':'python',
    }

print("The following languages have been mentioned:")

for language in favorite_languages.values():
 	print(language.title())
```
**剔除重复项可用*set*集合**

```
set去除重复项
favorite_languages = {
	'jen':'python',
	'sarah':'C',
	'edward':'ruby',
	'phil':'python',
    }

print("The following languages have been mentioned:")

for language in set(favorite_languages.values()):
 	print(language.title())
```

-------
### 嵌套
概念：将一系列字典存储在列表中，或将列表作为值存储在字典中
字典列表：
#### 列表中包含字典:

```
字典列表：列表中包含字典
aliens = []

for alien_number in range(30):
	new_alien = {'color':'red','point':5,'speed':'slow'}
	aliens.append(new_alien)

for alien in aliens[:5]:
	print(alien)
print("...")

print("Total number of aliens:" + str(len(aliens)))
```
#### 在字典中存储列表:
```
在字典中存储列表
pizza = {
	'crust':'thick',
	'toppings':['mushroom','extra cheese'],
    }

print("You ordered a " + pizza['crust'] + "-crust pizza " +
	"with the following toppings:")

for topping in pizza["toppings"]:
	print("\t" + topping)

```
```
favorite_languages = {
	'jen':['python','ruby'],
	'sarah':'C',
	'edward':['ruby','go'],
	'phil':['python','haskell'],
    }

for name,languages in favorite_languages.items():
	if len(languages) == 1:
		print("\n" + name.title() + " 's favorite languages is: \n\t" + languages)
	else:
		print("\n" + name.title() + " 's favorite languages are: ")
		for language in languages:
			print("\t" + language)
```
#### 在字典中存储字典:
```
在字典中存储字典
users = {
    'aeinstein':{
        'first':'albert',
        'last':'einstein',
        'location':'princeton',
        },

    'mcurie':{
        'first':'marie',
        'last':'curie',
        'location':'paris',
        },
    }

for username,user_info in users.items():
	print("\n" + username.title())
	full_name = user_info['first'] + " " + user_info['last']
	location = user_info['location']

	print("\tFull name: " + full_name.title())
	print("\tLocation: " + location.title())
```

-------

### 用户输入
`input()` 函数让程序暂停运行，等待用户输入一些文本，获取用户输入后，Python将其存储在一个变量中。
`int()` 函数将数字的字符串表示转换为数值表示。

```
height = input("How tall are you , in inches? ")
height = int(height)
if height >= 36:
    print("\nYou are tall enough to ride")
else:
    print("\nYou'll be able to ride when you're a little older.")
```

-------

### While
```
prompt = "\nTell me something, and I will repeat it back to you: "
prompt += "\nEnter 'quit' to end the program. "

message = ""
while message != 'quit':
    message = input(prompt)
    if message != "quit":
        print("\n"+ message)
```
使用标志:在要求很多条件都满足才继续运行的程序中，可定义一个变量，用于判断整个程序是否处于活动状态，这个变量被称为标志。

```
prompt = "\nTell me something, and I will repeat it back to you: "
prompt += "\nEnter 'quit' to end the program. "

active = True
while active:
    message = input(prompt)
    if message == "quit":
        active = False
    else:
        print("\n"+ message)
```
`break`退出循环
`continue`退出本次循环
`while`循环处理列表和字典
`for`循环是一种遍历列表的有效方式，但在for循环中不应修改列表，否则导致Python难以跟踪其中的元素
while循环可在遍历列表的同时对其进行修改。
#### 在列表之间移动元素：

```
unconfirmed_users = ['alice','brain','candace']
confirmed_users = []

while unconfirmed_users:
    current_user = unconfirmed_users.pop()
    print("Verifying user: " + current_user.title())
    confirmed_users.append(current_user)
print("\nThe following users have been confirmed: ")
for confirmed_user in confirmed_users:
    print(confirmed_user.title())
```
#### 使用用户输入填充字典：
```
responses = {}
polling_active = True

while polling_active:
    name = input("\nWhat's your name: ")
    response = input("Which mountain would you like to climb someday? ")

    responses[name] = response
    repeat = input("Would you like to let another person respond?(yes or no)")
    if repeat == 'no':
        polling_active = False
print("\n---Poll Result---")
for name,response in responses.items():
    print(name + " would like to climb " + response + ".")
```

-------
### 迭代器
概念：可以被`next()`函数调用并不断返回下一个值的对象称为`迭代器：Iterator`

可以直接作用于`for`循环的数据类型有以下几种：

一类是集合数据类型，如`list、tuple、dict、set、str`等；

一类是generator，包括`生成器`和带`yield`的generator function。

这些可以直接作用于for循环的对象统称为可迭代对象：Iterable。

可以使用`isinstance()`判断一个对象是否是Iterable对象：

```
>>> from collections import Iterable
>>> isinstance([], Iterable)
True
>>> isinstance({}, Iterable)
True
>>> isinstance('abc', Iterable)
True
>>> isinstance((x for x in range(10)), Iterable)
True
>>> isinstance(100, Iterable)
False
```

生成器都是Iterator对象，但list、dict、str虽然是Iterable，却不是Iterator。

把list、dict、str等Iterable变成Iterator可以使用iter()函数：

```
>>> isinstance(iter([]), Iterator)
True
>>> isinstance(iter('abc'), Iterator)
True
```
为什么list、dict、str等数据类型不是Iterator？

```
这是因为Python的Iterator对象表示的是一个数据流，Iterator对象可以被next()函数调用并不断返回下一个数据，直到没有数据时抛出StopIteration错误。可以把这个数据流看做是一个有序序列，但我们却不能提前知道序列的长度，只能不断通过next()函数实现按需计算下一个数据，所以Iterator的计算是惰性的，只有在需要返回下一个数据时它才会计算。

Iterator甚至可以表示一个无限大的数据流，例如全体自然数。而使用list是永远不可能存储全体自然数的。
```

Python的for循环本质上就是通过不断调用`next()`函数实现的，例如：

```
for x in [1, 2, 3, 4, 5]:
    pass
```

实际上完全等价于：

```
# 首先获得Iterator对象:
it = iter([1, 2, 3, 4, 5])
# 循环:
while True:
    try:
        # 获得下一个值:
        x = next(it)
    except StopIteration:
        # 遇到StopIteration就退出循环
        break
```
-------


### 函数
定义函数：def
文档字符串注释：””” “””
实参：调用函数时传递给函数的信息。
形参：函数完成其工作所需的一项信息。
位置实参：实参与形参按顺序一一对应。Python将按顺序将函数调用中的实参关联到函数定义中相应的形参。
关键字实参：传递给函数的名称-值对。

```
def describe_pet(animal_type,pet_name):
    print("\nI have a " + animal_type + ".")
    print("My " + animal_type + "'s name " + pet_name.title() + ".")
describe_pet(animal_type='hamster',pet_name='harry')
```
默认值：使用默认值时，在形参列表中必须先列出没有默认值的形参，再列出有默认值的实参。让Python依然能够正确地解读位置实参。

```
def describe_pet(pet_name,animal_type='dog'):
    print("\nI have a " + animal_type + ".")
    print("My " + animal_type + "'s name " + pet_name.title() + ".")
describe_pet(pet_name='harry')
```
返回值：函数返回的值被称为返回值。
实参可选：将实参指定一个默认值—空字符串

```
def get_formatted_name(first_name,last_name,middle_name=""):
    if middle_name:
        full_name = first_name + " " + middle_name + " "+ last_name
    else:
        full_name = first_name + " " + last_name
    return full_name.title()

musician = get_formatted_name('l','m',"j")
print(musician)

musician = get_formatted_name('l',"j")
print(musician)
```
返回字典：

```
def build_person(first_name,last_name):
    person = {'first':first_name,'last':last_name}
    return person
musician = build_person('l','mj')
print(musician)
```
传递任意数量的实参

```
def make_pizza(*toppings):
    print(toppings)

make_pizza('pepperoni')
make_pizza('mushroom','green peppers','extra cheese')
```
`*号让Python创建一个空元祖`
`* 任意数量的关键字实参`

```
def build_profile(first,last,**user_info):
    profile = { }
    profile['first_name'] = first
    profile['last_name'] = last
    for key,value in user_info.items():
        profile[key] = value
    return profile
user_profile = build_profile('l','mj',
                             location='beijing',
                             field='physics')
print(user_profile)

```
`**号让Python创建了一个空字典`
模块：将函数存储在独立文件中，是扩展名为.py的文件。
导入整个模块: `import  模块名`
`使用：module_name.function_name()`

导入特定的函数
`from  module_name import function_name,function2_name`
`使用：function_name()`

as 别名：给函数在导入时起别名
`from  module_name import function_name  as  别名`
`使用： 别名（）`

给模块指定别名:   `import  module_name as 别名`
`使用：别名.function_name()`

导入模块中的所有函数:  `from  module_name import *`
`使用：function_name()`

-------

### 类
创建类：`class  类名():`     （类名首字母大写）

方法__init__(self,形参..)：类中的函数称为`方法`，形参self必不可少，位于所有形参之前。Python调用__init__()函数创建实例时，将自动传入实参self，每个与类相关联的方法调用都自动传递实参self，他是一个指向实例本身的引用，让实例能够访问类中的属性和方法。

#### 使用类和实例

```
class Car():
    """ 一次模拟汽车的简单尝试"""
    def __init__(self,make,model,year):
        self.make = make
        self.model = model
        self.year = year
    def get_descriptive_name(self):
        long_name = str(self.year) + ' ' +self.make + ' ' + self.model
        return long_name.title()

my_new_car = Car('audi','a4',2016)
print(my_new_car.get_descriptive_name())
```

#### 给属性指定默认值

```
class Car():
    """ 一次模拟汽车的简单尝试"""
    def __init__(self,make,model,year):
        self.make = make
        self.model = model
        self.year = year
        self.odometer_reading = 0
    def get_descriptive_name(self):
        long_name = str(self.year) + ' ' +self.make + ' ' + self.model
        return long_name.title()
    def read_odometer(self):
        print("This car has " + str(self.odometer_reading) + " miles on it.")

my_new_car = Car('audi','a4',2016)
print(my_new_car.get_descriptive_name())
my_new_car.read_odometer()
```

#### 修改属性的值1：直接修改属性的值

```
class Car():
    """ 一次模拟汽车的简单尝试"""
    def __init__(self,make,model,year):
        self.make = make
        self.model = model
        self.year = year
        self.odometer_reading = 0
    def get_descriptive_name(self):
        long_name = str(self.year) + ' ' +self.make + ' ' + self.model
        return long_name.title()
    def read_odometer(self):
        print("This car has " + str(self.odometer_reading) + " miles on it.")

my_new_car = Car('audi','a4',2016)
print(my_new_car.get_descriptive_name())
my_new_car.odometer_reading = 23
my_new_car.read_odometer()
```

#### 修改属性的值2：通过方法修改属性的值

```
class Car():
    """ 一次模拟汽车的简单尝试"""
    def __init__(self,make,model,year):
        self.make = make
        self.model = model
        self.year = year
        self.odometer_reading = 0
    def get_descriptive_name(self):
        long_name = str(self.year) + ' ' +self.make + ' ' + self.model
        return long_name.title()
    def read_odometer(self):
        print("This car has " + str(self.odometer_reading) + " miles on it.")

    def update_odometer(self,mileage):
        if mileage >= self.odometer_reading:
            self.odometer_reading = mileage
        else:
            print("You can't roll back an odometer!")

my_new_car = Car('audi','a4',2016)
print(my_new_car.get_descriptive_name())
my_new_car.update_odometer(22)
my_new_car.update_odometer(20)
my_new_car.read_odometer()
```

#### 修改属性的值3：通过方法对属性的值进行递增

```
class Car():
    """ 一次模拟汽车的简单尝试"""
    def __init__(self,make,model,year):
        self.make = make
        self.model = model
        self.year = year
        self.odometer_reading = 0
    def get_descriptive_name(self):
        long_name = str(self.year) + ' ' +self.make + ' ' + self.model
        return long_name.title()
    def read_odometer(self):
        print("This car has " + str(self.odometer_reading) + " miles on it.")

    def update_odometer(self,mileage):
        if mileage >= self.odometer_reading:
            self.odometer_reading = mileage
        else:
            print("You can't roll back an odometer!")
    def increment_odometer(self,miles):
        self.odometer_reading += miles

my_new_car = Car('audi','a4',2016)
print(my_new_car.get_descriptive_name())
my_new_car.update_odometer(22)
my_new_car.read_odometer()
my_new_car.increment_odometer(100)
my_new_car.read_odometer()
```

### 导入类
导入一个或多个类：  `from 模块 import 类名1，类名2...`

导入整个模块：`import 模块`
使用：`模块.类`

导入模块中的所有类：`from 模块 import *`

-------
### 继承
一个类`继承`另一个类时，它将自动获得另一个类的所有属性和方法；原有类称为`父类`，新类称为`子类`。子类继承了其父类的所有属性和方法，同时还可以定义自己的属性和方法。

#### 子类的方法__init__()

```
class Car():
    """ 一次模拟汽车的简单尝试"""
    def __init__(self,make,model,year):
        self.make = make
        self.model = model
        self.year = year
        self.odometer_reading = 0
    def get_descriptive_name(self):
        long_name = str(self.year) + ' ' +self.make + ' ' + self.model
        return long_name.title()
    def read_odometer(self):
        print("This car has " + str(self.odometer_reading) + " miles on it.")

    def update_odometer(self,mileage):
        if mileage >= self.odometer_reading:
            self.odometer_reading = mileage
        else:
            print("You can't roll back an odometer!")
    def increment_odometer(self,miles):
        self.odometer_reading += miles

class ElectricCar(Car):
    """电动骑车的独特之处"""
    def __init__(self,make,model,year):
        super().__init__(make,model,year)

my_tesla = ElectricCar('tesla','model s',2016)
print(my_tesla.get_descriptive_name())
```
1.创建子类时，父类必须包含在当前文件中，且位于子类前面。
2.定义子类时，必须在括号内指定父类的名称。
3.super()帮助python将父类和子类关联起来。

#### 给子类定义属性和方法

```
class Car():
    """ 一次模拟汽车的简单尝试"""
    def __init__(self,make,model,year):
        self.make = make
        self.model = model
        self.year = year
        self.odometer_reading = 0
    def get_descriptive_name(self):
        long_name = str(self.year) + ' ' +self.make + ' ' + self.model
        return long_name.title()
    def read_odometer(self):
        print("This car has " + str(self.odometer_reading) + " miles on it.")

    def update_odometer(self,mileage):
        if mileage >= self.odometer_reading:
            self.odometer_reading = mileage
        else:
            print("You can't roll back an odometer!")
    def increment_odometer(self,miles):
        self.odometer_reading += miles

class ElectricCar(Car):
    """电动骑车的独特之处"""
    def __init__(self,make,model,year):
        super().__init__(make,model,year)
        self.battery_size = 70

    def describe_battery(self):
        print("This car has a  " + str(self.battery_size) + " -kWH battery")


my_tesla = ElectricCar('tesla','model s',2016)
print(my_tesla.get_descriptive_name())
my_tesla.describe_battery()
```

#### 重写父类的方法

当父类的方法不符合子类的要求时，可对其进行重写，在子类中定义一个方法，与父类方法同名。这样Python就不调用父类方法，只调用子类的方法。

```
class Car():
    """ 一次模拟汽车的简单尝试"""
    def __init__(self,make,model,year):
        self.make = make
        self.model = model
        self.year = year
        self.odometer_reading = 0
    def get_descriptive_name(self):
        long_name = str(self.year) + ' ' +self.make + ' ' + self.model
        return long_name.title()
    def read_odometer(self):
        print("This car has " + str(self.odometer_reading) + " miles on it.")

    def update_odometer(self,mileage):
        if mileage >= self.odometer_reading:
            self.odometer_reading = mileage
        else:
            print("You can't roll back an odometer!")
    def increment_odometer(self,miles):
        self.odometer_reading += miles

    def fill_gas_tank(self):
        print("This car  need a gas tank!")

class ElectricCar(Car):
    """电动骑车的独特之处"""
    def __init__(self,make,model,year):
        super().__init__(make,model,year)
        self.battery_size = 70

    def describe_battery(self):
        print("This car has a  " + str(self.battery_size) + " -kWH battery")
    def fill_gas_tank(self):
        print("This car doesn't need a gas tank!")


my_tesla = ElectricCar('tesla','model s',2016)
print(my_tesla.get_descriptive_name())
my_tesla.describe_battery()
my_tesla.fill_gas_tank()
```

#### 将实例用作属性

```
class Car():
    """ 一次模拟汽车的简单尝试"""
    def __init__(self,make,model,year):
        self.make = make
        self.model = model
        self.year = year
        self.odometer_reading = 0
    def get_descriptive_name(self):
        long_name = str(self.year) + ' ' +self.make + ' ' + self.model
        return long_name.title()
    def read_odometer(self):
        print("This car has " + str(self.odometer_reading) + " miles on it.")

    def update_odometer(self,mileage):
        if mileage >= self.odometer_reading:
            self.odometer_reading = mileage
        else:
            print("You can't roll back an odometer!")
    def increment_odometer(self,miles):
        self.odometer_reading += miles

    def fill_gas_tank(self):
        print("This car  need a gas tank!")
class Battery():
    """一次模拟电动汽车电瓶的简单尝试"""
    def __init__(self,battery_size = 70):
        self.battery_size = battery_size
    def describe_battery(self):
        print("This car has a  " + str(self.battery_size) + " -kWH battery")

class ElectricCar(Car):
    """电动骑车的独特之处"""
    def __init__(self,make,model,year):
        super().__init__(make,model,year)
        self.battery = Battery()


    def fill_gas_tank(self):
        print("This car doesn't need a gas tank!")


my_tesla = ElectricCar('tesla','model s',2016)
print(my_tesla.get_descriptive_name())
my_tesla.battery.describe_battery()
my_tesla.fill_gas_tank()
```

-------
#### Python 标准库
collections 模块下的 OrderedDict类可以实现有顺序的字典。

-------
#### 类编码风格
类名使用**驼峰命名**
实例名、模块名全部小写，并在单词之间加下划线

-------

### 文件
#### 从文件中读取数据：
##### 读取整个文件：
```
with open('../pi_digits.txt') as file_object:
    contents = file_object.read()
    print(contents.rstrip())
```
1. open(参数)：打开文件 返回的是文件对象
2. 关键字with在不再需要访问文件后将其关闭。
3. read(): 读取文件
4. 相比原始文件，输出多一个空行，因为read()到达文件末尾时返回一个空字符串，可以使用rstrip()函数删除。

##### 逐行读取：

```
filename = '../pi_digits.txt'
with open(filename) as  file_object:
    for line in file_object:
        print(line.rstrip())
```
##### 将文件各行内容存储在列表里

```
filename = '../pi_digits.txt'
with open(filename) as file_object:
    lines = file_object.readlines()

for line in lines:
    print(line.rstrip())
```
##### 使用文件的内容

```
filename = '../pi_digits.txt'
with open(filename) as file_object:
    lines = file_object.readlines()

pi_string = ''
for line in lines:
    pi_string += line.strip()

print(pi_string)
print(len(pi_string))
```
##### 写入空文件

```
filename = '../programming.txt'
with open(filename,'w') as file_object:
    file_object.write("I Love programming.")
    
with open(filename) as  file_object:
    content = file_object.read()
    print(content)
```
##### 写入多行

```
filename = '../programming.txt'
with open(filename,'w') as file_object:
    file_object.write("I Love programming.\n")
    file_object.write("I am mushroom.\n")
    
with open(filename) as  file_object:
    content = file_object.read()
    print(content)
```
##### 附加到文件（追加不覆盖）

```
filename = '../programming.txt'
with open(filename,'w') as file_object:
    file_object.write("I Love programming.\n")
    file_object.write("I am mushroom.\n")

with open(filename,'a') as  file_object:
    file_object.write("emmmmm......")
    
with open(filename) as  file_object:
    content = file_object.read()
    print(content)
```
##### 异常
try-except-else:
Python尝试执行try代码块中的代码，只有可能引发异常的代码才需要放在try语句中。有一些仅在try代码块成功执行时才需要运行的代码，放在else代码块中。except代码块告诉Python,如果尝试运行try代码块中的代码时引发了指定的异常，应该怎么去做。

split()：函数以空格为分隔符将字符串拆分成多个部分，并将这些部分都存储到一个列表中。

程序发生异常时，像什么都没发生一样继续执行，也不提示任何消息，可使用pass语句。
##### 存储数据（模块JSON）
**json.dump()**

```
import json
numbers = [2,3,5,7,11,13]

filename = "../number.json"
with open(filename, 'w') as f_obj:
    json.dump(numbers, f_obj)
with open(filename) as  f_obj:
    context = f_obj.read()
    print(context)
```
**json.load()**

```
import json

filename = '../number.json'
with open(filename) as file_object:
    numbers = json.load(file_object)
print(numbers)
```

-------
### 装饰器
概念：在代码运行期间动态增加功能的方式，称之为“装饰器”（Decorator）。






