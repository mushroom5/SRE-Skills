# Python

#  字符串
	* title() :以首字母大写的方式显示每个单词
	* upper() :全部大写
	* lower() :全部小写
	* '+' ：拼接
	* rstrip() :删除字符串末尾多余的空白
	* lstrip() :删除字符串开头多余的空白
	* strip() :删除字符串两头多余的空白
- - - -
# 数字
	* 整数：+ — * / （乘方） %（求模运算）
	* str() :将非字符串类型值转换成字符串
- - - -
# 注释
	* #
	* 目的：代码要做什么 如何做的
- - - -
# 列表
	* 概念：列表由一系列按特定顺序的元素组成。
	* 表示：[ ]
	* 特点:
	 1、有序的集合
	 2、通过偏移来索引，从而读取数据
	 3、支持嵌套
	 4、可变的类型
	* 修改列表元素：列表名[索引值] = 新值
	* 添加列表元素：
		* 在列表末尾添加元素：append()  列表名.append(需添加的元素)
		* 在列表中插入元素：insert()    列表名.insert(索引,需添加的元素)
	* 删除列表元素：
		* 已知要删除的元素在列表中的位置：del    del 列表名[索引]    ---删除之后无法访问
		* 删除列表末尾的元素：pop()   ---删除之后可保存在变量里继续访问
		* 删除任何列表中的元素：pop(索引)
		* 根据值删除元素：remove()
	* 组织列表：
		* 永久性排序：正序：sort()    反序：sort(reverse=True)
		* 临时排序：  sorted()
		* 倒着打印列表：reverse()
		* 确定列表的长度：len()
	* 遍历列表
		* for 循环    for item in 列表:
	* 创建数值列表
		* range()：生成一系列数字。
	`range(2,11,2) 从2开始，不断加2，直到达到或超过终值。`
		* list()：可是将range()的结果直接转换成列表。
		* min()：寻找列表最小值
		* max()：寻找列表最大值
		* sum()：列表元素和
		* 列表解析：
```列表解析
squares = [value**2 for value in range(1,11)]  
print(squares)
```
		* 切片：指定要使用的第一个元素和最后一个元素的索引
```切片
players = ['charles','martina','micheal','florence','eli']      print(players[1:3])
```
		* 遍历切片：
```遍历切片
for player in players[:3]:
print(player.title())
```
		* 复制列表:
	  创建一个包含整个列表的切片，同时省略起始索引和终止索引（[:]）
- - - -
# 元组
	* 不可变的列表被称为元组。
	* 表示: ( )
	* 虽然不能修改元组的元素，但是可以给存储元组的变量赋值。
- - - -
# IF
	* 条件测试:每条if语句的核心都是一个值为True或False的表达式，这种表达式被称为**条件测试**。
	* 检查是否相等： ==
	* 检查是否不相等：！=
	* 与：and
	* 或：or
	* 检查特定值是否包含在列表中：in
	* 检查特定值是否不包含在列表中：not in
	* if-elif-else
	* 检查列表是否为空:
```检查列表是否为空
requested_toppings = []
if requested_toppings:
	for requested_topping in requested_toppings:
		print("Adding" + requested_topping +".")
	print("\nFinished making your pizza")
else:
	 print("Are you sure you want a plain pizza?")
```
- - - -
#  字典
	* 概念：字典是一系列键值对，每个键都与一个值相关联。
	* 表示：{'key':'value',...}
	* 字典是一种动态结构。
	* 删除键值对：del 字典名['key']
	* 遍历字典：
		* 遍历所有的键-值对
```遍历所有的键-值对,items()
user_0 = {
	'username':'efermi',
	'first':'enrico',
	'last':'fermi',
    }

for key,value in *user_0.items():*
	print("\nKey: "+ key)
	print("\nValue: " + value)
```
		* 遍历字典中的所有键
```遍历字典中的所有键，keys()
favorite_languages = {
	'jen':'python',
	'sarah':'C',
	'edward':'ruby',
	'phil':'python',
    }

for name in favorite_languages.keys():
 	print(name.title())
```
		* 按顺序遍历字典中的所有键
```for循环中对返回的键进行排序，sorted()
favorite_languages = {
	'jen':'python',
	'sarah':'C',
	'edward':'ruby',
	'phil':'python',
    }

for name in sorted(favorite_languages.keys()):
 	print(name.title() + ", thanks you for taking the poll")
```
		* 遍历字典中的所有值
```遍历字典中的所有值，values()
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
::剔除重复项可用**set**集合::
```set去除重复项
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
	* 嵌套
		* 概念：将一系列字典存储在列表中，或将列表作为值存储在字典中
		* 字典列表：列表中包含字典
```字典列表：列表中包含字典
aliens = []

for alien_number in range(30):
	new_alien = {'color':'red','point':5,'speed':'slow'}
	aliens.append(new_alien)

for alien in aliens[:5]:
	print(alien)
print("...")

print("Total number of aliens:" + str(len(aliens)))
```
		* 在字典中存储列表
```在字典中存储列表
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
		* 在字典中存储字典
```在字典中存储字典
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
- - - -
# 用户输入
* input() 函数让程序暂停运行，等待用户输入一些文本，获取用户输入后，Python将其存储在一个变量中。
* int() 函数将数字的字符串表示转换为数值表示。
```
height = input("How tall are you , in inches? ")
height = int(height)
if height >= 36:
    print("\nYou are tall enough to ride")
else:
    print("\nYou'll be able to ride when you're a little older.")
```
- - - -
# While
```
prompt = "\nTell me something, and I will repeat it back to you: "
prompt += "\nEnter 'quit' to end the program. "

message = ""
while message != 'quit':
    message = input(prompt)
    if message != "quit":
        print("\n"+ message)
```
* 使用标志:在要求很多条件都满足才继续运行的程序中，可定义一个变量，用于判断整个程序是否处于活动状态，这个变量被称为标志。
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
* break退出循环
* continue退出本次循环
* while循环处理列表和字典
for循环是一种遍历列表的有效方式，但在for循环中不应修改列表，否则导致Python难以跟踪其中的元素
while循环可在遍历列表的同时对其进行修改。
在列表之间移动元素：
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
使用用户输入填充字典：
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

