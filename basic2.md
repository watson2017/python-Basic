### 一、多线程
```
import time, datetime
import threading
print("start of program...")

def test():
    print(datetime.datetime.now().strftime('%Y-%m-%d %H:%M:%S'),
          "Action: sleep..")
    time.sleep(5)
    print(datetime.datetime.now().strftime('%Y-%m-%d %H:%M:%S'),
          "Action:wake up")

threadObj = threading.Thread(target=test)
threadObj.start()
print("Enf of program")
---
start of program...
2018-01-17 17:22:21 Action: sleep..
Enf of program
2018-01-17 17:22:26 Action:wake up
```

向线程的目标函数中传递参数
```
>>> import threading
>>> threadObj = threading.Thread(target=print,args=['Cats','Dogs','Frogs'],kwargs={'sep':'&'})
>>> threadObj.start()
Cats&Dogs&Frogs
```

从python中启动其他的程序
```
from subprocess import Popen
Popen(r"C:\Program Files\Sublime Text 3\sublime_text.exe")
```

### 二、类的简单使用

1.基础类
```
class Dog():
    def __init__(self, age, name):
        self.age = age
        self.name = name

    def DescribeDog(self):
        print("My Dog's name is %s and now it is %s years old." %
              (self.name.title(), self.age))


MyDog = Dog("1", "dahuang")
MyDog.DescribeDog()
-----
My Dog's name is Dahuang and now it is 1 years old.
```

2.父类、子类及类的调用
```
# ================================1.car 的父类================================
class Car():
    def __init__(self, make, model, years):
        """make:生产商，model：型号，years：生产年限"""
        self.make = make
        self.model = model
        self.years = years
        self.odometer_reading = 0  # 设置一个参数，汽车跑的总里程数，初始值为0，无需外界传入

    def get_descriptive_name(self):
        long_name = str(self.years) + ',' + self.model + ',' + self.make
        return long_name.title()    

    def read_odometer(self):
        # self.odometer_reading = 23
        print("this car has " + str(self.odometer_reading) + " miles on it.")

    def update_odometer(self, newmiles):
        """
            将里程表读数设定为指定的值
            禁止将里程表的读数往回拨
        """    
        # self.odometer_reading = newmiles
        if self.odometer_reading <= newmiles:
            self.odometer_reading = newmiles
        else:
            print("you can not rollback an old meter !")

# ======================2.子类的创建======================================
# 创建子类时，父类必须包含在当前文件中，且位于子类前面
# 创建子类的实例时，Python首先需要完成的任务是给父类的所有属性赋值
# super()是一个特殊函数，帮助Python将父类和子类关联起来
# =========================================================================
class ElectricCar(Car):  # 括号中object表示从哪里继承父类
    def __init__(self, make, model, years):
        super().__init__(make, model, years)  # 继承父类的属性(其中的方法)，与Python2 版本中写法不一样
        self.battery = Battery(66)              # 调用Battery类

    def read_odometer(self):
        """重写父类的方法：在子类中定义一个与要重写的父类方法同名。这样，Python就不会继承这个父类方法"""
        print("elc car not need read miles.")


# ============================3.将实例用作属性==================================
# 将类的一部分作为一个独立的类提取出来，可以将大型类拆分成多个协同工作的小类
# 如下方的Battery实例可以用作ElectricCar类的一个属性
# ==============================================================================
class Battery():
    def __init__(self, battery_size=100):
        """初始化电池的容量"""
        self.battery_size = battery_size

    def describe_battery(self):
        """描述电池剩余量"""
        print("this electriccar has a " + str(self.battery_size) + " -kWh battery.")

my_car = Car('benci', 'hhhh', 2017)
elc_car = ElectricCar('aodi', 'yy', 2018)
print(my_car.get_descriptive_name())
print(elc_car.get_descriptive_name())
elc_car.read_odometer()
# my_car.odometer_reading = 50
my_car.update_odometer(50)
my_car.read_odometer()
elc_car.battery.describe_battery()  # 调用3中的battery类
```
- [github地址:](https://github.com/watson2017/usage-class.git)

### 三、JSON 对象
>JSON(JavaScript Object Notation) 是一种轻量级的数据交换格式，易于人阅读和编写。
- json.dumps 	将 Python 对象编码成 JSON 字符串
- json.loads	将已编码的 JSON 字符串解码为 Python 对象

>**Note**: json.dumps()与json.dump()的区别在于`json.dumps()`用于将dict类型的数据转成str，`json.dump()`用于将dict类型的数据转成str,并写入到json文件中,同理,json.loads()是用于将str类型的数据转成dict, json.load()用于从json文件中读取数据。

![python 原始类型向 json 类型的转化对照表.png](http://upload-images.jianshu.io/upload_images/6868814-8ee2091c0702f2ea.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


**Eg1：json.dumps()和json.loads()的简单应用举例**
```
import json
data = {'a': '1111', 'b': '2222', 'c': '3333', 'd': '4444'}
jsDumps = json.dumps(data)
jsLoads = json.loads(jsDumps)
print(data, type(data), jsDumps, type(jsDumps), jsLoads, type(jsLoads), sep='\n')
---
{'c': '3333', 'b': '2222', 'd': '4444', 'a': '1111'}
<class 'dict'>
{"c": "3333", "b": "2222", "d": "4444", "a": "1111"}
<class 'str'>
{'c': '3333', 'b': '2222', 'd': '4444', 'a': '1111'}
<class 'dict'>

# 如果想要数据展示的美观点，可以添加点其他参数如缩进，排序等
print(json.dumps(data, sort_keys=True, indent=4, separators=(',', ':')))
-----
{
    "a":"1111",
    "b":"2222",
    "c":"3333",
    "d":"4444"
}
```

**Eg2： json.load()和json.dump()的应用举例。**

```
#!/usr/bin/env python
# coding=utf-8
"""
文档的功能：把用户名字记录到json文件中，当用户第二次打开时，检测到json文件中有该内容,就会直接将json文件中的内容反馈给用户。
"""    
import json

def get_stored_username():
    """如果存储了用户名，就获取它"""
    filename = 'username.json'
    try:
        with open(filename) as f_obj:
            username = json.load(f_obj)
    except FileNotFoundError:
        return None
    except ValueError:
        return None
    else:
        return username

def get_new_username():
    """提示用户输入用户名"""
    filename = 'username.json'
    username = input("What is your name? ")
    with open(filename, 'w') as f_obj:
        json.dump(username, f_obj)
    return username


def Welcome_user():
    """问候用户，并指出其名字"""
    username = get_stored_username()
    if username:
        print("Welcome back, " + username + "!")
    else:
        username = get_new_username()
        print("We'll remember you when you come back, " + username + "!")


Welcome_user()
```
