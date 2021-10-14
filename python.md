# python基础

## 1. 注释

适当的对代码进行注释说明

### 单行注释

一般情况下注释是在代码的上面书写的

如：

```
 # 这是一个注释

	print('hello')

```

### 多行注释

以` ``` `开始，并以` ``` `结束



## 2. 变量以及数据类型

### 2.1 变量的定义

定义：` 变量名 = 变量值`(等号的作用是赋值)

``` python
# 定义一个变量表示这个字符串。如果需要修改内容只需要修改变量对应的值即可
weather = "今天天气真好"
print(weather)	# 变量名不需要引号
```

说明：

- 变量即可变化的量，可随时进行修改。
- 程序就是用来处理数据的，而变量就是用来存储数据的。

### 2.2 变量的类型

**Number	数值**

- int : money = 5000
- float : money1 = 1.2



**boolean	布尔**

- 流程控制语句
- 性别的变量（使用的单词是sex    gender)

  ```  
  # 男	True
  sex = True
  gender = False
  ```

​		

**string	字符串**

字符串使用的是单引号或双引号

` s = 'abc' `

` s1 = "你好" `



**list	列表**

应用场景：当获取到很多个数据的时候那么我们可以将他们存储到列表中然后直接使用列表访问

`name_list = ['周杰伦' , '科比']`



**tuple	元组**

`age_tuple = (18,19,20,21)`



**dict	字典**

应用场景：scrapy框架

格式：变量名 = {key:value,key1:value1}

`person = {'name' : '老王' , 'age' : 81}`



### 2.3 查看数据类型

type方法判断变量的数据类型

格式：`type(变量)`



## 3. 标识符和关键字

计算机编程语言中，标识符是用户编程时使用的名字，用于给变量、常量、函数、语句块等命名，以建立起名称与使用之间的关系。、

1. 标识符由字母、下划线和数字组成，且数字不能开头。
2. 严格区分大小写。
3. 不能使用关键字。

### 3.1 命名规范

- 标识符命名要做到顾名思义。

``` python
name = "zhangsan"
age = 23
```

- 遵守一定的命名规范
  - 驼峰命名法，又分为大驼峰和小驼峰命名法
- 小驼峰：第一个单词以小写字母开始；第二个单词的首字母大写，例如：myName、aDog
- 大驼峰：每个单词的首字母都采用大写字母，例如：MyName.



### 3.2 关键字

- 关键字：一些具有特殊功能的标识符。

`  False、None、True、and、as、assert、break、class、continue、def、del、elif、else、except、finally、for、from、global、if、import、in、is、lambda、nonlocal、not、or、pass、raise、return、try、while、with、yield  `



## 4. 类型转换

### 4.1 转换为int型

- str --> int 

``` python
a = '123'
print(type(a))
# 将字符串转换为整数
b = int(a)
print(type(b))
```

- float --> int

``` py
a = 1.23
print(type(a))
# 将float转为整数只返回整数部分
b = int(a)
print(b)
print(type(b))
```

  - boolean --> int

```python
# 强制类型转换为谁就写什么方法
# True --> 1    False --> 0
a = True
print(type(a))
b = int(a)
print(b)
print(type(b))
```



### 4.2 转换为float型

```python
# 当爬虫的时候大部分获取的数据都是字符串类型

a = '12.34'
print(type(a))
# 将字符串类型数据转换为浮点数
b = float(a)
print(b)
print(type(b))
```



### 4.3 转换为字符串型

```python
# 整型转换为字符串  大部分应用场景

a = 80
print(type(a))
# 强制类型转换为字符串的方法是str()
b = str(a)
print(b)
print(type(b))
```

```python
# 布尔类型转换为字符串
a = True
print(type(a))
b = str(a)
print(b)		# 输出 True
print(type(b))
```



### 4.4 转换为布尔类型

- int --> bool

```python
# 如果对非0的整数(int	包含正数和负数)进行bool类型的转换那么全都是True
a = 1
print(type(a))
# 将整数变成布尔类型的数据
b = bool(a)
print(b)	# 输出True
print(type(b))
```

```python
a = 0
print(type(a))
# 在整数范围内0强制类型转换为bool类型的结果是False
b = bool(a)
print(b)
print(type(b))
```

- float --> bool

```python
# 将浮点数转换为bool类型的数据的时候正浮点数和负浮点数的结果是True
# 如果是0.0那么结果是False
a = 1.0
print(type(a))
b = bool(a)
print(b)
print(type(b))
```

- str --> bool

```python
# 只要字符串中有内容那么在强制类型转换为bool的时候就返回True，否则返回False
a = '哈哈哈'
print(type(a))
b = bool(a)
print(b)
print(type(b))
```

- list --> bool

```python
# 只要列表中有数据那么强制类型转换为bool的时候就返回True
a = ['张三', '李四', '王五']
print(type(a))
b = bool(a)
print(b)
print(type(b))
# 如果列表中什么数据都没有的情况下返回False
a = []
print(type(a))
b = bool(a)
print(b)
print(type(b))
```

- tuple --> bool

```python
# 只要元组中有数据那么强制类型转换为bool的时候就返回True
a = ('张三','李四','王五')
print(type(a))
b = bool(a)
print(b)
print(type(b))
# 如果元组中什么数据都没有的情况下返回False
a = ()
print(type(a))
b = bool(a)
print(b)
print(type(b))
```

- dic --> bool

```python
# 只要字典中有数据那么强制类型转换为bool的时候就返回True
a = {'name':'张三'}
print(type(a))
b = bool(a)
print(b)
print(type(b))

# 如果字典中什么数据都没有的情况下返回False
a = {}
print(type(a))
b = bool(a)
print(b)
print(type(b))
```

注：什么情况是False

```python
print(bool(0))
print(bool(0.0))
print(bool(''))
print(bool(""))
print(bool([]))
print(bool(()))
print(bool({}))
```



## 5. 运算符

### 5.1 算数运算符

```python
a = 3
b = 2
print(a + b)
print(a - b)
print(a * b)
print(a / b)
# 整除(取整)
print(a // b)
# 取余
print(a % b)
# 指数(a的b次幂)
print(a ** b)

print((5+1) * 2)
```

> 注意：运算时`**`优先级>`* / % //`>`+ -`

```python
# 字符串的加法是进行拼接的
a = '123'
b = '456'
print(a + b)

# 在python中 +两端都是字符串才可以加法运算
a = '123'
b = 456
# print(a + b)
print(a + str(b))

# 字符串的乘法是将字符串重复多少次
a = '你好'
print(a * 3)
```



### 5.2 赋值运算符

| 运算符 | 描述       | 实例                                                   |
| ------ | ---------- | ------------------------------------------------------ |
| =      | 赋值运算符 | 把=右边的结果赋给左边的变量，如num=1+2*3，结果num值为7 |

```python
# 同时为多个变量赋值(使用等号连接)
b = c = 20
print(b)
print(c)
# 多个变量赋值(使用逗号分隔)
d,e,f = 1,2,3
print(d)
print(e)
print(f)
```



### 5.3 复合赋值运算符

`+=	-=	*=	/=	//=	%=	**=`

```python
a = 1
a += 2  # a = a + 2
print(a)

b = 1
b *= 3  # b = b * 3
print(b)

c = 2
c -= 1  # c = c - 1
print(c)

d = 3
d /= 2  # d = d / 2
print(d)

e = 3
e //=2  # e = e // 2
print(e)

f = 3
f %= 5  #    f = f % 5
print(f)

g = 5
g **=3  #   g = g ** 3
print(g)
```



### 5.4 比较运算符

`# 比较运算符 ==	!=	>	>=	<	<=`

```python
# 比较运算符返回的都是boolean类型的数据

# == 恒等     判断==两边的变量是否一致
a = 10
b = 20
print(a == b)   # False

# != 不等     判断!=两边的变量是否不一致
a = 10
b = 20
print(a != b)   # True

# > 大于(小于同理)
print(10>20)
print(10>5)

# >= 大于等于
print(10 >= 10)
print(10 >= 5)
print(10 >= 20)
```



### 5.5 逻辑运算符

```python
# 逻辑运算符 and(与) or(或)  not(非)
# and 与
# and两边的数据必须全部都是True的时候才会返回True，只要有一端返回的是False，那么就返回False
# and两边都是False的时候返回False
print(10 > 20 and 10 > 11)
# and一端是True，一端是False，返回的是False
print(10 > 5 and 10>11)
# and一端是False，一端是True，返回的是False
print(10 > 11 and 10 > 5)
# and两端都是True，返回的是True
print(10 > 5 and 10 > 6)

# or 或者
# or的两端只要有一端是True就返回True，否则返回False
# or的两端都是False，则返回False
print(10 > 20 or 10 > 21)
# or的两端前面的是True，后面的是False，返回True
print(10 > 5 or 10 > 20)
# or两端都是True，则返回True
print(10 > 5 and 10 > 6)

# not 非(取反)
print(not True)
print(not False)
print(not (10 > 20))
```



and：短路与

or：短路或

```python
a = 36
a > 10 and print('hello world')
# and的性能优化 当and前面的结果是False的情况下那么后面的代码就不再执行了
a < 10 and print('hello world')

# or的性能优化
# or 只要有一方为True 那么结果就是True
a = 38

a > 39 or print('你好')
```



## 6. 输入输出

### 6.1 输出

```python
# 普通输出
print('啊啊啊')

# 格式化输出
# scrapy框架的时候   excel文件 mysql redis
age = 18
name = '老王'

# %s 代表的是字符串    %d 代表的是数值
print('我的名字是%s,我的年龄是%d' % (name,age))
```



### 6.2 输入

```python
# 普通输出
print('啊啊啊')

# 格式化输出
# scrapy框架的时候   excel文件 mysql redis
age = 18
name = '老王'

# %s 代表的是字符串    %d 代表的是数值
print('我的名字是%s,我的年龄是%d' % (name,age))

password = input('请输入您的银行卡密码')
print('我的密码是：%s' % password)

name = input('请输入您的名字')
print('我的名字是：%s' % name)
```



## 7. 流程控制语句

### 7.1 if判断语句

```python
 if关键字的语句结构
 if 判断条件：
       代码（如果判断条件为True的时候执行if下面的内容）
```

```python
age = 17

# 如果您的年龄大于18 那么你就可以开车了
if age > 18:
    print('你可以开车了')

# True代表男   False表示女
sex = True
if sex == True:
    # if下面的代码必须是一个tab键或四个空格
    print('你是一个男性')
```

#### if练习

```python
# 在控制台输入一个年龄，如果您的年龄大于18那么打印你可以去网吧了

# input返回的是字符串类型
age = input('请输入您的年龄：')

# 字符串和整数int是不可以比较的
if int(age) > 18:
    print('你可以去网吧了')
```



### 7.2 ifelse

```python
# ifelse的语法
# if 判断条件:
#       判断条件为True的时候执行的代码
# else:
#       判断条件为False的时候执行的代码

age = 17
if age > 18:
    print('你可以去网吧了')
else:
    print('回家写作业去吧')
```

#### ifelse练习

```python
# 在控制台输入一个年龄，如果您的年龄大于18那么打印你可以去网吧了，否则输出 回家写作业去吧
age = input('请输入您的年龄') # age = int(intput('请输入您的年龄'))
if int(age) >= 18:										
    print('你可以去网吧了')
else:
    print('回家写作业去吧')
```



### 7.3  elif

```python
# 在控制台输入您的分数
# >=90优秀 80-90良好 70-80中等 60-70及格 <60不及格
score = int(input('请输入您的成绩：'))

if score >= 90:
    print('优秀')
elif score >= 80:
    print('良好')
elif score >= 70:
    print('中等')
elif score >= 60:
    print('及格')
else:
    print('不及格')
```



### 7.4 for

```python
# 循环字符串
s = 'china'
# i是字符串中一个又一个的字符的变量
# s是代表的是要遍历的数据
for i in s:
    print(i)
```

```python
# range(5)
# range方法的结果 一个可以遍历的对象
# range(5) 0-4  [0,5)
for i in range(5):
     print(i)
        
# # range(1,6)
# # range(起始值，结束值)
# # [1,6)
# for i in range(1,6):
#     print(i)

# range(1,10,3)
# range(起始值，结束值，步长)
# 1  4  7  10
#  [1,10)
# for i in range(1,10,3):
#     print(i)
```

```python
# 应用场景  会爬取一个列表返回给我们
# 循环一个列表
a_list = ['王','刘','李']
# 遍历列表中的元素
# for i in a_list:
#     print(i)

# 遍历列表中的下标

# 判断列表中的元素的个数
# print(len(a_list))
# 0 1 2
for i in range(len(a_list)):
    print(i)
```



## 8. 数据类型高级

### 8.1 字符串高级

```python
# len 长度    len函数可以获取字符串的长度
s = 'china'
print(len(s))

# find：查找内容    查找指定内容在字符串中是否存在，如果存在就返回该内容在字符串中第一次出现的位置
s1 = 'china'
print(s1.find('c'))

# startswith,endswith：判断    判断字符串是不是以什么开头/结尾(是输出True，不是输出False)
s2 = 'china'
print(s2.startswith('c'))
print(s2.endswith('a'))

# count：计算某些字符出现的次数     返回 str在start和end之间在 mystr里面出现的次数
s3 = 'aaabb'
print(s3.count('a'))
print(s3.count('b'))

# replace：替换内容      替换字符串中指定的内容，如果指定次数count，则替换不会超过count次。replace('旧','新')
s4 = 'cccdd'
print(s4.replace('c','d'))

# split：切割字符串       通过参数的内容切割字符串(split('切割的字符')
s5 = '1#2#3#4'
print(s5.split('#'))

# upper,lower：修改大小写     将字符串中的大小写互换
s6 = 'china'
print(s6.upper())

s7 = 'CHINA'
print(s7.lower())

# strip：去除空格
s8 = '   a   '
print(len(s8.strip()))
```



### 8.2 列表高级

列表的增删改查

#### 添加元素

- append在末尾添加元素
- insert在指定位置插入元素
- extend合并两个列表

```python
# append  追加    在列表的最后来添加一个对象/数据
food_list = ['铁锅炖大鹅','酸菜五花肉']
print(food_list)

food_list.append('小鸡炖蘑菇')
print(food_list)

# insert 插入
char_list = ['a','c','d']
print(char_list)
# index的值就是你想插入数据的那个下标
char_list.insert(1,'b')
print(char_list)

# extend    可以将另一个列表中的元素逐一添加到列表中
num_list = [1,2,3]
num1_list = [4,5,6]

num_list.extend(num1_list)
print(num_list)
```

#### 修改元素

```python
city_list = ['北京','上海','广州','深圳']

print(city_list)

# 将列表中的元素的值修改
# 可以通过下标来修改，注意列表中的下标是从0开始的
city_list[2] = '河北'
print(city_list)
```

#### 查找元素

包含以下几个方法：

- in和not in

```python
# in是判断某一个元素是否在一个列表中
food_list = ['锅包肉','地三鲜','乱炖']

# 判断一下在控制台输入的数据是否在列表中
food = input('请输入您想吃的食物')

if food in food_list:
    print('在')
else:
    print('不在，想什么呢')

# not in判断某一个元素是否不在一个列表中

ball_list = ['篮球','足球']
# 在控制台上输入你喜欢的球类然后判断是否不在这个列表中
ball = input('您喜欢的球类：')
if ball not in ball_list:
    print('不在')
else:
    print('在')
```

#### 删除元素

列表元素的常用删除方法有：

- del： 
- pop：删除最后一个元素
- remove：根据元素的值进行删除

```python
a_list = [1,2,3,4,5]
print(a_list)

# 根据下标进行删除列表中的元素
# 爬取的数据中有个别的数据是我们不想要的那么可以通过下标删除
del a_list[2]
print(a_list)
```

```python
b_list = [1,2,3,4,5]
# pop删除列表中的最后一个元素
b_list.pop()
print(b_list)
```

```python
c_list = [1,2,3,4,5]
print(c_list)                 # 输出 [1,2,3,4,5]
# 根据元素的值进行删除列表中的数据
c_list.remove(3)
print(c_list)                 # 输出 [1,2,4,5]
```



### 8.3 元组高级

python的元组与列表类似，不同之处在于**元组的元素不能修改**。元组使用()，列表使用[]。

```python
a_tuple = (1,2,3,4)
print(a_tuple[0])
# 元组是不可以修改里面的内容的
# a_tuple[3] = 5
# print(a_tuple)      # 报错



a_list = [1,2,3,4]
a_list[3] = 5
print(a_list)             # 输出[1,2,3,5]
# 列表中的元素是可以修改的而元组中的元素是不可以被修改的
```

 定义只有一个数据的元组，需要**在唯一的元素后写一个逗号**

```python
a_tuple = (5)
print(type(a_tuple))         # int类型

# 当元组中只有一个元素的时候那么他是整型数据
# 定义只有一个数据的元组，需要在唯一的元素后写一个逗号
b_tuple = (5,)
print(type(b_tuple))        # tuple类型
```



### 8.4 切片

切片是指对操作对象截取其中一部分的操作。**字符串、列表、元组**都支持切片操作。

切片的语法：[起始:结束:步长]，也可简化使用[起始:结束]

注意：选取的区间从“起始”位开始，到“结束”位的前一位结束（不包含结束位本身），步长表示选取间隔。

```python
s = 'hello world'

# 在切片中直接写一个下标
print(s[0])

# 包含左边的数据不包含右边的数据
print(s[0:4])

# 是从起始的值开始一直到末尾
print(s[1:])

# 从下标为0的索引元素开始一直到第二个参数为止    遵循左闭右开
print(s[:4])

# hello world
# 从下标为0的位置开始到下标为6的位置结束，每次增长2个长度
print(s[0:6:2])
```

### 8.5 字典高级

**查看元素**

```python
# 定义一个字典
person = {'name':'老王','age':28}

# 访问person的name
print(person['name'])
print(person['age'])

# 使用[]的方式，获取字典中不存在的key的时候会发生异常 keyerror
# print(person['sex'])

# 不能使用.的方式来访问字典的数据
# print(person.name)

print(person.get('name'))
print(person.get('age'))

# 使用.的方式，获取字典中不存在的key的时候会返回None值
print(person.get('sex'))
```

**修改元素**

```python
person = {'name':'张三','age':'18'}

# 修改之前的字典
print(person)

# 修改name的值为法外狂徒
person['name'] = '法外狂徒'

# 修改之后的字典
print(person)
```

**添加元素**

```python
person = {'name':'老王'}
print(person)

# 给字典添加一个新的key value
# 如果使用变量名字['键'] = 数据时 这个键如果在字典中不存在那么就会变成新增元素
person['age'] = 18

# 如果这个键在字典中存在那么就会变成这个元素
person['name'] = '阿马'
print(person)
```

**删除元素**

```python
# del
#   (1) 删除字典中指定的某一个元素
person = {'name':'老王','age':18}

# 删除之前
print(person)

del person['age']
print(person)


#   (2) 删除整个字典
# 删除之前
print(person)
del person
# 删除之后
print(person)


# clear
#   (3) 清空字典但是保留字典对象
print(person)

# 清空指的是将字典中的所有数据都删除掉而保留字典的结构
person.clear()
print(person)
```

**遍历**

```python
# 遍历-->就是数据一个一个的输出

person = {'name':'阿马','age':18,'sex':'男'}
# (1) 遍历字典的key
# 字典.keys()方法 获取字典中所有的key值    key是一个变量的名字我们可以随便起
for key in person.keys():
    print(key)
# (2) 遍历字典的value
# 字典.values()方法 获取字典中所有的value值      key是一个变量的名字我们可以随便起
for value in person.values():
    print(value)

# (3) 遍历字典的key和value
for key,value in person.items():
    print(key,value)

# (4) 遍历字典的项/元素
for item in person.items():
    print(item)
```



## 9. 函数

### 9.1 定义函数

``` python
def 函数名():
    代码
```

例：

```python
# 定义函数
def f1():
    print('欢迎光临')
    print('男宾三位')
    print('欢迎下次光临')
```

### 9.2 调用函数

定义了函数之后，就相当于有了一个具有某些功能的代码，想要让这些代码能够执行，需要调用它。

调用函数：通过**函数名()**即可完成调用

```python
# 调用函数，定义完函数后，函数不会自动执行需要手动调用它
f1()
```

> 每次调用函数时，函数都会从头开始执行，当这个函数中的代码执行完毕后，意味着调用结束了。

### 9.3 函数参数

```python
 使用函数计算1和2的和

def sum():
    a = 1
    b = 2
    c = a + b
    print(c)

sum()



def sum(a,b):
    c = a + b
    print(c)

# 位置参数  按照位置一一对应的关系来传递参数
sum(1,2)
sum(100,200)

# 关键字传参(不推荐)
sum(b = 200,a = 100)


# 定义函数的时候 sum(a,b)  我们称a和b为形式参数简称形参
# 调用函数的时候 sum(a,b)  我们称1和2为实际参数简称实参
```

### 9.4 函数返回值

返回值就是程序中函数完成一件事情后，最后给调用者的结果

```python
# 返回值的关键字是return，存在函数中

def buyIceCream():

    return '冰淇淋'

# 使用一个变量来接收函数的返回值
food = buyIceCream()

print(food)
```

```python
# 案例练习
# 定义一个函数然后让函数计算两个数值并且返回计算之后的结果
def sum(a,b):
    c = a + b
    return c

a = sum(123,456)
print(a)
```

### 9.5 局部变量

```python
# 局部变量：在函数的内部定义的变量我们称之为局部变量
# 特定：其作用域范围是函数内部，而函数外部是不可以使用的

def f1():
    # 函数的内部定义的变量我们称之为局部变量
    a = 1
    print(a)
f1()
print(a)
```

### 9.6 全局变量

```python
# 全局变量：定义在函数的外部的变量我们称之为全局变量
# 特点：可以在函数的外部使用，也可以在函数的内部使用

a = 1
print(a)

def f1():
    print(a)

f1()

# 在满足条件的情况下要使用作用域最小的那个变量范围
```



## 10. 文件

### 10.1 文件的打开与关闭

**打开文件/创建文件**

在python中，使用open函数，可以打开一个已经存在文件，或者创建一个新文件

open(文件路径，访问模式)

例：

``` python
 f = open('test.txt', 'w')
```

```python
# 创建一个test.txt文件

# open(文件路径，访问模式)
# 模式：   w 可写
#         r 可读
# open('test.txt','w')

# 打开文件
fp = open('test.txt','w')
fp.write('hello world')

# 文件夹是不可以创建的    暂时需要手动创建
fp = open('demo/text.txt','w')
fp.write('hello cuc')

# 文件的关闭
fp = open('a.txt','w')
fp.write('hello')
fp.close()
```

### 10.2 文件的读写

```python
# 写数据
# write方法

fp = open('test.txt','a')

fp.write('hello world\n' * 5)

fp.close()

# 如果再次运行这段代码    会打印10次还是5次呢?
# 如果文件存在会先清空原来的数据然后再写
# 我想在每一次执行之后都要追加数据
# 如果模式变成了a 那么就会执行追加的操作
```

```python
# 读数据
fp =open('test.txt','r')
# 默认情况下 read是一字节一字节的读效率比较低
content = fp.read()
print(content)

# readline是一行一行的读取  但只能读取一行
content = fp.readline()
print(content)

# readlines可以按行来读取  但是会将所有的数据都读取到   并且以一个列表的形式返回
# 而列表的元素 是一行一行的数据
content = fp.readlines()
print(content)
```

### 10.3 序列化和反序列化

通过文件操作，我们可以将字符串写入到一个本地文件。但是如果是一个对象（例如列表、字典、元组等）就无法直接写入到一个文件里，需要对这个对象进行序列化，然后才能写入到文件里。

设计一套协议，按照某种规则，把内存中的数据转换为字节序列，保存到文件，这就是序列化，反之，从文件的字节序列恢复到内存中就是反序列化。

**对象--> 字节序列 （序列化）**

**字节序列-->对象  （反序列化）**

Python中提供了JSON这个模块用来实现数据的序列化和反序列化。



**JSON模块**

JSON(JavaScriptObjectNotation,JS对象简谱)是一种轻量级的数据交换标准。JSON的本质是字符串。

**使用JSON实现序列化**

JSON提供了dump和dumps方法，将一个对象进行序列化。

dumps方法的作用是把对象转换为字符串，它本身不具备将数据写入文件的功能。



```python
# 序列化的两种方式
# dumps()
# (1)创建一个文件
fp = open('test.txt','w')

# (2)定义一个列表
name_list = ['zs','ls']

# 导入json模块到该文件中
import json

# 序列化
# 将python对象变成json字符串
# 我们在使用scrapy框架的时候  该框架会返回一个对象  我们要将对象写入到文件中    就要使用json.dumps
names = json.dumps(name_list)

# 将names写入到文件中
fp.write(names)
fp.close()



# dump
# 在将对象转换为字符串的同时，指定一个文件的对象然后把转换后的字符串写入到这个文件里

fp = open('test.txt','w')

name_list = ['zs','ls']

import json
# 相当于names = json.dumps(name_list)和fp.write(names)
json.dump(name_list,fp)
fp.close()
```

```python
# 反序列化
# 将json的字符串变成一个python对象

fp = open('test.txt','r')

content = fp.read()

# 读取之后是字符串类型的
print(content)
print(type(content))

# loads
import json

json.loads(content)
# 将json字符串变成python对象
result = json.loads(content)
print(result)
print(type(result))


# load

fp = open('test.txt','r')

import json

result = json.load(fp)

print(result)
print(type(result))
fp.close()
```



## 11. 异常

程序在运行过程中，由于我们的编码不规范或者其他原因，导致我们的程序无法继续运行，此时程序就会出现异常。如果我们不对异常进行处理，程序可能会由于异常直接中断掉。为了保证程序的健壮性，我们在程序设计里提出了异常处理这个概念。

### 11.1 读取文件异常

```python
# 异常的格式
# try:
#     可能出现异常的代码
# except  异常的类型
#     友好的提示

try:
    fp = open('text.txt','r')
    fp.read()
except FileNotFoundError:
    print('系统正在升级，请稍后再试。。。')
```

