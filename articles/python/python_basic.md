因为想做一个小程序，数据来源网易云音乐，也就是需要使用python来爬取数据(也许有其他办法爬取数据)。开始学习略微观望了的python，记录整个学习过程。

python之禅：Now is better than never.</br>
《Python编程:从入门到实践》——基础知识</br>

我的环境—win10
# 安装
版本选择——python3
安装方式
- 官网下载python(stable)版本——
- 安装anaconda
  - conda是一个包管理器和环境管理器。你可以创建多个环境，每个环境中使用不同版本的包。例如可以在一个环境中安装python2，另一个环境安装python3,然后只需要切换环境就可以运行你编写的不同的版本的代码。作为一个js开发者，想到了NVM，你可以使用安装不同版本的node，然后根据实际需要切换版本。
  - anaconda是GUI工具，用命令行conda完成的操作，可以在GUI中简单完成
  - 下载地址——[国内镜像](https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/)

验证安装完成</br>
- 如果直接安装了python，在命令中输入python，会出现>>>从而进入python运行环境
- 如果安装了anaconda,需要运行anaconda prompt，把它当作命令行工具使用。输入python,会出现>>>从而进入运行环境。

问题</br>
- 使用anaconda navigator,create新环境时报错OPENSSL_sk_new_reserv
  - 打开anaconda安装目录下DLLs文件夹，并找到libssl-1_1-x64.dll,注意修改时间。
  - 打开anaconda/Library/bin目录，找到libssl-1_1-x64.dll
  - 比较两者的修改时间。就是因为不一致导致的问题，所以需要将DLLs文件下的libssl-1_1-x64.dll拷贝到anaconda/Library/bin目录下进行替换
- 创建环境过程很慢(这跟npm安装一样，需要设置一个国内的镜像地址)
  - 在anaconda navigator中Environments，右侧界面有channel，有一个默认的配置，选择添加https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/

在VS Code中配置python环境——部分译自[vscode配置python环境的文档](https://code.visualstudio.com/docs/python/environments)
- 搜索安装插件“python”
- `Ctrl+Shift+P`打开Command Palette，输入`python:select interpreter`
- 弹出的窗口会列出所有可用全局环境、conda环境和虚拟环境的列表——图片可去上面的给出的vscode文档链接中查看
- 选择上面列表中的你所需要的一项，在settings.json中设置python.pythonPath。如果你只有一个环境，可以在user settings中设置，这个设置在所有vscode编辑的项目使用。如果你只想在当前项目中使用某个环境，在workspace Settins中设置。`Ctrl+Shift+P`打开Command Palette,输入`preferences:open User settings`或者`preferences:open Workspace settings`。
- 防止运行程序时自动激活当前选定的环境，可以设置`"python.terminal.activateEnvironment": false`
```
{
    "python.pythonPath": "D:\\ProgramFiles\\anaconda\\python.exe",
    "python.terminal.activateEnvironment": false
}
```
- 配置完成之后，创建一个hello.py文件，可以在vscode的左下角看到配置的pythonPath。如果想要改变，可以点击该区域重新选择环境。
[示图]
- 右键——Run python File in terminal,terminal会打印出你写的代码结果
- **注意**：在打开的terminal上进行conda install \<package\>或者pip install 操作都是针对当前环境的持久性操作

# 语法
## 变量与简单数据类型
```python
message = "Hello Python world!"
print(message)
```
变量命名规则：
- 变量只能包含字母、数字和西下划线。可以字母或者下划线打头，不能以数字打头
- 变量名不能有空格
- 不能使用python关键字或者函数名作为变量名
- 变量名应该简短且具有描述性
- 慎用小写字母i和大写字母O，因为它们可能被人错看成数字1和0</br>
- 实践：尽量避免使用大写字母
#### 字符串
- 字符串可以使用单引号和双引。</br>

方法举例：str.title()——以首字母大写的方式显示每个单词
- 字符串拼接——使用+(加号)。
- 使用制表符(\t)或者换行符(\n)添加空白。
- 删除字符串开头或者结尾的空白
  - 删除结尾空白str.rstrip()
  - 开头空白str.latrip()
  - 两头空白str.strip()
  - **修改变量之后需要将变量存回变量才可以有效改变该变量**,
```python
str = ' python '
print(str) #' python '
print(str.lstrip()) #'python '
print(str)#' python '
str = str.lstrip()
print(str)#'python '
```
- str()函数，将非字符串值表示为字符串——以避免类型错误
#### 注释
python中使用#添加注释。

## 列表
**创建列表**
```python
names=['anna','nicholas','jamie']
print(names) #['anna','nicholas','jamie']
```
**访问元素**
```python
print(names[0])  #anna
print(names[-1]) # jamie
print(names[-2]) # nicholas
```
下标从0开始</br>
最后一个元素可以使用下标-1，倒数第二个使用-2</br>
**修改元素**
```python
names[0]='Jane'
print(names) #['Jane','nicholas','jamie']
```
**添加元素**
```python
names.append('Anna')
print(names) #['Jane','nicholas','jamie','Anna']
names.insert(0,'Harry')
print(names) #['Harry','Jane','nicholas','jamie','Anna']
```
**删除元素**
```python
del names[0] #删除指定下标元素
names.pop() # 删除最后一个元素，并返回该元素
names.pop(0) #删除指定下标的元素，并返回该元素
names.remove('Jane') #删除值为Jane的元素，且只删除第一个
```
**元素排序**
```python
names.sort() #字母顺序a-b-c
names.sort(reverse=true) #与上面相反的顺序
sorted(names) #返回排序的列表，不改变names
names.reverse() #将列表元素翻转
```
**列表长度**
```
len(names)
```
## 操作列表
**循环遍历列表**
```python
names=['anna','nicholas','jamie']
for name in names:
    print(name)
    print(name.title()) #与上一行相同缩进，都在for中执行
print('--------------') #缩进与for相同，不在for中执行
```
缩进不对，会造成语法错误或者逻辑错误，一定要注意。</br>
**数值列表**
```python
for n in range(1,5):
    print(n) 
#1
#2
#3
#4

nums = list(range(2,10,2))  # 2开始，不断加2，直到达到10或者超过10
print(nums) # [2,4,6,8,10]

print(min(nums)) #2
print(max(nums)) #8
print(sum(nums)) #20

squares = [value**2 for value in range(1,11)]
print(squares) #[1,4,9,16,25,36,49,64,81,100]
```
**切片与复制**
```python
nums = [2,4,6,8,10]
nums1 = nums[1:]  #[4,6,8,10]，从1开始，到结束
nums2 = nums[:1]  #[2],从0开始，不包括1
nums3 = nums[:]   #[2,4,6,8,10] 从头到尾复制
```
**元组**</br>
Python将不能修改的值成为不可变的，而不可变的列表被称为元组。
```python
dimensions = (200,50) #使用圆括号，列表使用的是方括号
dimensions = (100,30) # 可以修改整个变量
dimensions[0] = 100 # TypeError，不能修改单个元素
for d in dimensions: # 遍历
    print(d)
```

## if语句
```python
cars = ['audi','bmw','subaru','toyota']
for car in cars:
    if car == 'bmw':
        print(car.upper()) #函数不改变car的值
    else:
        print(car.title())
```
== 用来判断是否相等，区分大小写</br>
其他比较：!=,<,>,<=,>= </br>
**多个条件**</br>
使用and或者or</br>
```
condition1 and condition2
condition1 or condition2
```
**检查某个值是否在或不在列表**</br>
```python
'audi' in cars # True
'marie' not in cars #False
```
**布尔表达式**</br>
```python
game_active = True
can_edit = False
```
**if-else结构**</br>
**if-elif-else结构**</br>
elif可使用多次，进行多个判断</br>
**if-elif结构**</br>
可以省略else，使用elif可以更清楚的表示条件</br>
**确保列表不为空**</br>
```python
cars = []
if cars:
    print(cars) #如果列表不为空，打印出来
```

## 字典
python的字典是一系列键-值对。键都与一个值对应，使用键访问与之相关联的值。值可以数字、字符串、列表乃至字典。事实上，可以任何python对象用作字典值。</br>
```python
aliens = {} # 空字典
aliens = {'color':'red','points':5} #定义字典
print(aliens['color']) # 访问字典
aliens['y_position'] = 0 #添加字典元素
del aliens['y_position'] # 永久删除一个键值对

#书写格式
languages = {
    'jen':'python',
    'sarah':'c',
    'edward':'ruby'
}
print("sarah's favorite language is " +
        languages['sarah'].title()+
        ".")
```
**遍历字典**</br>
```python
#key,value可以换为person,language
for key,value in languages.items(): 
    print(key)
    print(value)

#遍历所有键
for key in languages.keys()

# 按照顺序遍历所有键
for key in sorted(languages.keys())

# 遍历所有值
for value in languages.values()

# 遍历不重复的值
for value in set(languages.values())
# set是集合，所有元素都不重复
```
**嵌套**</br>
```python
# 字典列表，列表项为字典
language1 = {"name":'python'}
language2 = {"name":'java'}
language3 = {"name":'javascript'}
languages = [language1,language2,language3]
print(languages)

# 字典中存储列表
languages ={
    'sarah':['python','javascript'],
    'anna':['java','ruby']
}

# 字典嵌套字典
users={
    'aein':{
        'first':'albert',
        'last':'einstein',
        'location':'princeton'
    }
}
```
## 用户输入与while循环
#### 用户输入
```python
message = input("enter your name:")#显示在终端，要求输入，输入的值存在message中
print("Hello "+message)
# enter your name: jamie
# Hello jamie

# input的输入是字符串
# 可以使用int()将字符串转化成数字
int(age)
#求模运算(余数)
n%m  == 0
```
#### while循环
```python
num = 1
while num <= 5:
    print(num)
    num+=1
#1 
#2
#3
#4
#5

# 让用户选择退出
prompt = "\nTell me something,I will repeat it back to you:"
prompt += "\nEnter quit to end the program."
message =""
while message != "quit":
    message = input(prompt)
    print(message)

# 可以使用一个标志（布尔值）来表示决定是否退出
# 判断输入的值，变换标志为True或者False
```
**break**可以退出当前循环。</br>
**continue**返回到循环开头，根据条件测试结果决定是否继续执行循环。

#### while循环处理字典和列表
for循环用来遍历列表，不应该在for循环中修改列表，这样会导致Python难以跟踪其中的元素。（这样的道理也适用于其他语言，没这么想过）
```python
names = [1,2,3,4]
while names: #不断循环，直至names变为空
    print(names.pop())
    
pets = ['dog','cat','dog','cat','rabbit','cat']
while 'cat' in pets: # 直到列表中没有cat为止
    pets.remove('cat')
print(pets)
```
**使用输入填充字典**</br>
```python
responses ={}
pooling_active = True
while pooling_active:
    name = input("\nwhat is your name?")
    response = input("which mountain would you like to climb someday?")
    responses[name] = response
    repeat = input("would you like to let another person respond?(yes/no)")
    if repeat == 'no':
        pooling_active = False
print("\n ---- poll results ---")
for name,response in responses.items():
    print(name+" would like to climb "+response)
```

## 函数
函数是带有名字的独立代码块。</br>
#### 定义函数
```python
def greet_user():  #关键字def，函数名greet_user
    """显示简单的问候语""" #文档字符串，用来说明函数的用途
    print("Hello")
greet_user() #使用函数
```
####  传递参数
```python
def greet_user(username):
    """显示简单的问候语"""
    print("Hello "+username.title())
greet_user("anna")
```
#### 位置实参</br>
形参和实参根据顺序一一对应。
#### 关键字实参
```Python
# 参数是一对名称——值对
greet_user(username ="anna")
```
#### 默认值
可以给形参指定默认值，如果给定了实参，函数将使用实参；如果没有给实参，将使用形参的默认值。</br>
```python
def greet_user(username="Jamie"):

# 默认参数必须放在最后，否则SynxError。这也是一种更好的形式
def greet_user(firstname,lastname="Micheal")
```
#### 避免实参错误
如果定义了形参，一定要传递实参进去，不然会报错。

#### 返回值
函数可以返回任何类型的值，包括字典和列表等较复杂的数据结构
```python
#返回简单值
def greet_user(lastname,firstname="Jamie"):
    """显示简单的问候语"""
    fullname = firstname+' '+lastname
    return fullname.title()
print(greet_user("Micheal","jamie"))

#返回字典
#
```
#### 让实参可选
```python
def greet_user(lastname,firstname,middle=''): # middle可选
    """显示简单的问候语"""
    if middle:
        fullname = firstname+' '+middle+' '+lastname
    else:
        fullname = firstname+' '+lastname
    return fullname.title()
```
#### 传递列表
传递列表给函数，函数内部访问其内容。
```python
def greet_user(names):
    """向列表中的用户发出简单的问候语"""
    for name in names:
        print(name)
```
在函数中修改列表
```python
names = ['william','Ben','sam']
finish_names =[]
def greet_user(names):
    """向列表中的用户发出简单的问候语"""
    while names:
        temp_name = names.pop() #删除
        print(temp_name)
        finish_names.append(temp_name) #加入已经问候过的列表中
greet_user(names)
print(names) # []
print(finish_names) # ['sam','william','Ben']
```
**禁止**函数修改列表</br>
```python
#只向函数函数列表的副本
function_name(list_name[:])
```
#### 传递任意数量的参数
```python
#toppings保存传递的任意数量的参数
def make_pizza(size,*toppings): 
    """概述要制作的pizza"""
    print("\nMaking a "+ str(size)+" pizza with the following toppings:")
    for topping in toppings:
        print("-"+topping)
make_pizza(12,'pepperoni')
make_pizza(16,'mushrooms','green peppers','extra cheese')
```
#### 传递任意数量的关键字参数
```python
# **双星号让python创建一个名为user_info的空字典
def build_profile(first,last,**user_info):
    """创建一个字典，包含我们知道的有关用户的一切"""
    profile = {}
    profile['first_name'] = first
    profile['last_name'] = last
    for key,value in user_info.items():
        profile[key] =value
    return profile
user_profile = build_profile('albert','einstein',
                             location='princeton',
                             field='physics')
print(user_profile)
```
#### 模块
将函数存储在被成为模块的独立文件中，再将模块导入到主程序中。import语句允许在当前运行的程序文件中使用模块中的代码。</br>
```python
import pizza # 导入整个模块
pizza.make_pizza(16,'pepperoni')
pizza.make_pizza(12,'mushroom','green peppers','extra cheese')
```
import pizza打开pizza.py文件，将其中的函数复制到这个程序中。Python在幕后复制这些代码。
```python
#从模块导入特定函数fun1,fun2,fun3
from moduleName import fun1,fun2,fun3
# 使用as重命名导入函数
from moduleName import fun1 as fn
# 导入模块中的所有函数
from moduleName import *
```
#### 函数编写指南
函数应包含阐述其功能的注释，注释紧跟在函数定义后面。</br>
给形参指定默认值时，等号两边不要有空格:
`def fun(parameter_0,parameter_1='default value')`</br>
函数调用中的关键字实参，等号两边同样不要有空格。</br>
所有import语句都应放在文件开头，唯一例外的情形是，在文件开头使用了注释描述整个程序。</br>

## 类
定义类，类属性，类方法。创建实例，访问实例属性，访问实例方法，用方法改变属性。
```python
class Car():
    def __init__(self,make,model,year):
        """初始化描述汽车的属性"""
        self.make = make
        self.model = model
        self.year = year
        #给属性指定默认值
        self.odometer_reading=0
    def read_odometer(self):
        """打印一条指出汽车里程的消息"""
        print("This Car has "+str(self.odometer_reading)+" miles on it.")        
    def update_odometer(self,mileage):
        """将里程表读数设置为指定的值"""
        if mileage >= self.odometer_reading:
            self.odometer_reading=mileage
        else:
            print("You can't roll back an odometer!")
    def increment_odometer(self,miles):
        """将里程数增加指定量"""
        self.odometer_reading  +=miles
        
#创建实例        
my_new_car = Car('audi','a4','2016')
#访问属性——点访问属性
print(my_new_car.make)#audi
print(str(my_new_car.odometer_reading))#0
#调用方法
my_new_car.read_odometer()#This Car has 0 miles on it.
#修改属性的值
my_new_car.odometer_reading= 23
my_new_car.read_odometer()#This Car has 23 miles on it.
#使用方法修改属性值
my_new_car.update_odometer(30)
my_new_car.read_odometer()#This Car has 30 miles on it.
my_new_car.update_odometer(10)#You can't roll back an odometer!
#使用方法递增属性值
my_new_car.increment_odometer(100)
my_new_car.read_odometer()#This Car has 130 miles on it.
```
#### 继承
在子类的__init__()中使用super()函数，帮助Python将父类和子类关联起来。</br>
```python
#继承Car
class ElectricCar(Car):
    """电动车的独特之处"""
    def __init__(self,make,model,year):
        """初始化父类的属性"""
        super().__init__(make,model,year)

my_tesla = ElectricCar('tesla','model s',2016)
print(my_tesla.get_descriptive_name())
```
子类继承父类后，可添加区分子类和父类所需的新属性和方法，也可以重写父类的方法——定义同名方法</br>
```python
class ElectricCar(Car):#父类Car
    """电动车的独特之处"""
    def __init__(self,make,model,year):
        """初始化父类的属性"""
        #使用super()继承Car
        super().__init__(make,model,year)
        #子类添加属性
        self.battery_size=70 
    # 子类添加方法
    def describe_battery(self): 
        """打印一条描述电瓶容量的消息"""
        print("This Car has a "+str(self.battery_size)+"-kWh battery.")
    # 重写父类方法，定义一个与父类同名的方法
    def fill_gas_tank(self):
        """电动汽车没有油箱"""
        print("This cat doesn't need a gas tank!")
my_tesla = ElectricCar('tesla','model s',2016)
print(my_tesla.get_descriptive_name())
```python
将实例用作属性
```python
# Battery
class Battery():
    """电瓶"""
    def __init__(self,battery_size=70):
        """初始化"""
        self.battery_size = battery_size
    def describe_battery(self): 
        """打印一条描述电瓶容量的消息"""
        print("This Car has a "+str(self.battery_size)+"-kWh battery.")
        
class ElectricCar2(Car):
    """电动汽车的独特之处"""
    def __init__(self,make,model,year):
        """初始化父类的属性，再初始化电动汽车特有的属性"""
        super().__init__(make,model,year)
        # Battery的实例用作属性
        self.battery = Battery()
print("测试")
my_tesla = ElectricCar2('tesla','model s',2016)
print(my_tesla.get_descriptive_name())
my_tesla.battery.describe_battery()
```

#### 导入类
将类存储在模块中，然后在主程序中导入所需的模块</br>
```python
from car import Car
#在car.py文件中有多个类
from car import ElectricCar
#导入多个类
from car import Car,ElectricCar
#导入整个模块
import car
car.Car('audi','beetle',2016)
car.ElectricCar('tesla','roadster',2016)
#导入模块的所有类——不推荐
from module_name import *
# 在一个模块中导入另一个模块
from car import Car
```
#### Python标准库
```python
from collections import OrderedDict
# OrderedDict与普通字典的区别，记录了添加顺序
```

## 文件与异常
#### 读取文件
```python
with open('./pi_digits.txt') as file_object:
    contents = file_object.read()
    print(contents)
```
只有打开文件，才能访问它。open()函数接收一个参数：要打开的文件名。open()返回一个表示文件的对象。

with在不再需要访问文件后将其关闭。让Python自动关闭文件。

read()方法读取了文件的全部内容，将其作为一个长长的字符串存储在变量contents中。
```python
open(file_path)
#文件路径——相对路径或者绝对路径

with open('./pi_digits.txt') as file_object:
    lines = file_object.readlines() #所有行存储在列表
for line in lines:
    print(line.rstrip())
pi_string = ''
for line in lines:
    pi_string+=line.strip() #将所a有行数据组织成一个字符串
print(pi_string)
print(len(pi_string))
# 判断字符串是否函数有888
if '888' in pi_string:
    print("pi_string has 888")
```
#### 写入文件
opem(filename,'w')</br>
以写入模式(w)打开文件，还可以用读取模式(r)，附加模式(a)或者读取和写入(r+)。</br>
如果文件不存在，open函数将自动创建它。</br>
写入模式会清空该文件。</br>
附加模式不会清空文件，在文件末尾增加。</br>
```python
with open(file_name,'a') as file_object:
    file_object.write("I love programmming!\n")
    file_object.write("I love creating new games!\n")
```
#### 异常
Python在程序出现错误时，创建一个异常对象。</br>
异常使用try-except代码块处理。</br>
```python
try:
    print(5/0)
except ZeroDivisionError:
    print("You can't divide by zero!")
```
**try-except-else**代码块,Python执行try代码块中代码，只有可能引发异常的代码才需要放在try语句中。try成功以后执行的代码放在else代码块中。except代码块告诉Python当try代码块引发了异常后应该怎么办。

```python
#文件打开异常
filename = 'alice.txt'
try:
    with open(filename) as f_obj:
        contents = f_obj.read()
except FileNotFoundError:
    print("Sorry,the file "+filename+" doesnot exist")
```
忽略异常——pass
```python
except FileNotFoundError:
    pass #出现异常时什么都不做
```
#### 存储数据
json模块能够将简单的Python数据结构转存到文件中，并在程序再次运行时加载该文件的数据。还可以使用json在Python程序之间分享数据。
```python
import jsonc
numbers =[2,3,5,7,11,13]
filename = 'numbers.json'
with open(filename,'w') as f_obj:
    json.dump(numbers,f_obj)# dump将数字列表存到文件中
```
```python
import json
# load加载json文件中的数据
with open(filename) as f_obj:
    numbers = json.load(f_obj)
print(numbers)
```
## 测试代码
使用python的unittest测试代码</br>
#### 测试函数
```python
import unittest
from name_func import get_name,other
class NamesTest(unittest.TestCase):
    """测试name_func.py"""
    def test_get_name(self):
        """测试是否能够正确的XXX"""
        name = get_name('janis','joplin')
        self.assertEqual(name,"Janis Joplin")
    def test_other(self):
        name = other()
        self.assertEqual(name,'some')
unittest.main() #运行整个文件中的测试
```

#### 测试类
方法 | 用途
---- |--
assertEqual(a,b) | 核实 a==b
assertNotEqual(a,b)|合适a!=b
assertTrue(a)|核实x为True
assertFalse(a)|核实x为False
assertIn(item,list)|核实item在list中
assertNotIn(item,list)|核实item不在list中



</br>
</br>
<font color=gray size=1>gray</font>
<font color=gray size=2>gray</font>
<font color=gray size=3>gray</font>
<font color=gray size=4>gray</font>

</br>
</br>

## 后备
目前还没使用到的部分，备用</br>
1、[vs code中python的debug配置相关](https://code.visualstudio.com/docs/python/debugging)</br>
2、[conda document](https://conda.io/projects/conda/en/latest/index.html)</br>
3、在python官网成功的python案例——激起你学习的欲望</br>
4、python资源大全——[中文版](http://jobbole.github.io/awesome-python-cn/)</br>
5、electron [编写一个markdown](https://juejin.im/post/5cfcd269e51d4510b71da5d2)</br>
6、eletron中文[学习记录](https://juejin.im/post/5c46ab47e51d45522b4f55b1#heading-49)
7、[python3.8.1中文文档](https://docs.python.org/zh-cn/3/)
8、[python百度百科——条目看起来很有用](https://baike.baidu.com/item/Python/407313)