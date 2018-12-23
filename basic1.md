# 第二章  控制流

## 一、"类真"和"类假"的值：
> 在其他的数据类型中的某些值，条件认为它们等价于True和False，在用于条件时，0、0.0、和''(空字符串)被认为是False，其他值被认为是True
```
for x in range(1,10,2):   # 1是初始值，10是结束值，2是步长
	print(x)
```
## 二、随机数
```
import random
print(random.randint(1,10)) #产生一个1到10的整数
a = ['aa','bb','cc']
random.sample(a,2)   # 表示在列表a中随机取出两列
```
## 三、提前结束程序
1.方式：sys.exit()

## 四、round、abs函数

1. round(a,n)  #四拾伍入函数,a是浮点数，n是保留的位数
```
 >>> round(100.123456,2) # 浮点数100.123456 取小数点后2位
100.12
```
2. abs(a)返回绝对值
```
>>> abs(100.123456)
100.123456
>>> abs(-100.123456)
100.123456
```
# 第三章、函数

## 一、print的使用
print的使用，主要包括换行符和分隔符，使用事例如下：
```
>>> print('hello', end='') # 不换行
hello>>>
>>> print('hello')
hello
>>> print('hello', end=',') # 以逗号作为换行符
hello,>>>

print('cats', 'dogs', 'mice', sep=',') #替换分隔符为逗号，默认的分隔符是空格
cats,dogs,mice
print('cats', 'dogs', 'mice', sep=' ')
cats dogs mice
```

# 第四章  列表
## 一、列表值的范围
1.列表的边界：
```
spam[1:4]  # 表示从spam[1]到spam[3],即左边的包括右边的不包括
```
## 二、列表的增删改查等操作

1.删除列表中的值，使用del
```
del spam[2]  # 2是列表中值的下标

#如果不知道其下标可以使用remove如：
spam.remove('bat')
```
2.查询列表的下标
```
spam.index('hello') # 查询spam中查找第一个'hello'的下标
```
3. 列表的连接
```
>>> a = ['1','2','3']
>>> b = ['a','b','c']
>>> c = a + b ;  print(c)  
['1', '2', '3', 'a', 'b', 'c']
>>> c = a*2 ; print(c)
['1', '2', '3', '1', '2', '3']
```
4.列表的添加
```
>>> spam = ['a','b','c']
>>> spam.append('d') ; spam  # 在列表的末尾添加'd'
['a', 'b', 'c', 'd']
>>> spam.insert(1,'y') ; spam # 在列表的下标1 处添加'y', 原下标1处的值往后移动
['a', 'y', 'b', 'c', 'd']
```
5.列表的替换
```
>>> spam = ['a','b','c']
>>> spam[1]='xxx' ; spam
['a', 'xxx', 'c']
```
6.列表的排序
```
spam.sort() # 如果是数值或者是字符串的列表可以使用sort()方法排序
spam.sort(reverse=True) # 让sort()按逆序排序

# sort()方法对字符串排序时，使用"ASCII字符顺序进行排序",而不是实际的字典排序
# 如果需要按照普通的字典顺序进行排序，需要在调用sort()方法时，将关键字参数key设置为str.lower
spam = ['Aaa', 'Bbb', 'aaa', 'cCc']
spam.sort()
print(spam)
spam.sort(reverse=True)
print(spam)
spam.sort(key=str.lower)
print(spam)
---
['Aaa', 'Bbb', 'aaa', 'cCc']
['cCc', 'aaa', 'Bbb', 'Aaa']
['aaa', 'Aaa', 'Bbb', 'cCc']
```
7.列表的引用
   当将列表赋给一个变量时，实际上是将列表的"引用"赋给了变量，引用是一个值，指向某些数据。类似于c 语言中的指针。例如：
```
spam = ['Aaa', 'Bbb', 'aaa', 'cCc']
test = spam
test[1] = 'jjj'
print(spam, test, sep=',')
---
['Aaa', 'jjj', 'aaa', 'cCc'],['Aaa', 'jjj', 'aaa', 'cCc']
```
8.列表的复制
当仅仅只是想要复制原来的列表并不想改变原有的列表，可以使用copy.copy()模块，如果`列表中包含列表`就需要使用`copy.deepcopy()`模块
```
from copy import copy,deepcopy
spam1 = ['Aaa', 'Bbb', 'aaa']
spam2 = ['Aaa', 'Bbb', 'aaa', ['111', '222']]
test = copy(spam1)
test2 = deepcopy(spam2)
test[1] = 'jjj'
test2[1] = 'yyy'
print(spam1, "\n", test)
print(spam2, "\n", test2)
---
['Aaa', 'Bbb', 'aaa'] 
['Aaa', 'jjj', 'aaa']
['Aaa', 'Bbb', 'aaa', ['111', '222']] 
['Aaa', 'yyy', 'aaa', ['111', '222']]
```

## 三、类似列表的类型：字符串和元祖
>列表并不是唯一表示序列值的数据类型。字符串和列表实际上很相似，可以认为`字符串是单个文本字符的列表`，对列表的很多操作也可以作用于字符串。但不同的是，列表是"可变的"数据类型,它的值可以添加，删除或者改变,然后字符串是"不可变的"，无法被更改。“元组”数据类型几乎与列表的数据类型一样。元组的输入用"()"，而不是"[]"，最重要的一点区别在于`元组像字符串一 样其值是不可被改变的`。如果需要一个永远不会改变的值的序列，就使用元组。
```
元组如：
eggs = ('hello', 42, 0.5)
 ```
# 第五章 字典和结构化数据

>- 像列表一样，"字典"是很多值的集合，但不像列表的下标，字典的索引可以使用许多不同的数据类型，不只是整数。字典的索引被称为"键"，键及其关联的值成为"键-值"对。字典的输入带"{}"。
>- 字典的表项是`不排序`的
>- 字典有三个方法，它们将返回类似列表的值，分别对应于字典的键、值和键-值对:keys(),values(),items(),这些方法返回的值不是真正的列表，不能别修改，对应的数据类型分别为:dict_keys,dict_values和dict_items

1.keys(),values(),items()
```
spam = {'color': 'red', 'age': '99'}
print(spam['color'])     #针对特定的键值获取其values值
print(spam.items())
print(spam.keys())
print(spam.values())
---
red
dict_items([('color', 'red'), ('age', '99')])
dict_keys(['color', 'age'])
dict_values(['red', '99'])
```
2.检测key或者value是否存在字典中
```
if 'xxxx' in spam.values():
	print("ok")
if 'yyyy' in spam.keys():
	print("ok")	
```
3.get 方法
>get()，有两个参数，第一个是键值，第二个是备用值，即如果键值不存在则返回备用值例如：
```
spam = {'color': 'red', 'age': '99'}
print(spam.get('age', 'none'))
print(spam.get('meiyou', 'none'))
---
99
none
```
4.setdefault()方法
>setdefault()为一个键设置一个默认值，如果字典中存在该键则返回原有的值，如果不存在则字典中就添加setdefault()设置的键值对。例如：
```
spam = {'color': 'red', 'age': '99'}
spam.setdefault('age', '6666')
print(spam)
spam.setdefault('sex', 'f')
print(spam)
---
{'age': '99', 'color': 'red'}
{'age': '99', 'color': 'red', 'sex': 'f'}
```
5.检测字符串中字符出现的次数
```
from pprint import pprint,pformat
message = 'this is a test message.'
count = {}
for x in message:
    count.setdefault(x, 0)
    count[x] += 1
pprint(count)      
# 使用pprint.pprint()模块可以使字典中的表项的显示比print()的输出结果更干净;
# 如果不需要打印出来而仅仅是想获得一个漂亮格式的字符串，可以使用pformat(),如test = pformat(count)
---
{' ': 4,
 '.': 1,
 'a': 2,
 'e': 3,
 'g': 1,
 'h': 1,
 'i': 2,
 'm': 1,
 's': 5,
 't': 3}
```
# 第六章  字符串操作

## 一、常用的字符串操作方法 
>upper(): 所有小写字母转大写，得到一个新字符串
lower(): 所有大写字母转小写，得到一个新字符串
isupper(): 判断是否有字母并且字母全是大写
islower(): 判断是否有字母并且字母全是小写
```
message = 'this is a test message.'
print(message.upper())
print(message.isupper(), message.upper().isupper(), sep=',')
---
THIS IS A TEST MESSAGE.
False,True
```
## 二、其他的isX字符串判断方法见《python 编程快速上手》第100页
>isalpha()        # 判断字符串只包含字母并且非空                                                                                        
isalnum()        # 判断字符串只包含字母和数字，并且非空
isdecimal()      # 判断字符串只包含数字字符，并且非空
isspace()        # 判断字符串只包含空格、制表符和换行，并且非空
istitle()        # 判断字符串仅包含以大写字母开头、后面都是小写字母的单词

## 三、字符串方法startswith()和endswith()
```
# 区分大小写
message = 'this is a test message.'
print(message.startswith('this'), message.endswith('Message.'))
---
True False
```

##  四、字符串方法 join()和 split()
>-  join()方法将一个字符串列表的值连起来成为一个独立的字符串，`调用join()方法的字符串将被插到列表参数中每个字符串的中间`。
>- split()方法与join()相反，针对一个字符串列表调用返回一个字符串列表。默认按照`空白字符`进行分割,split('xxx') 以'xxx'作为分隔符。
```
例子：
message = 'this is a test message.'
a = ['1', '2', '3']
result = ','.join(message)
result2 = 'hh'.join(a)
print(result, result2, sep='\n')
---
t,h,i,s, ,i,s, ,a, ,t,e,s,t, ,m,e,s,s,a,g,e,.
1hh2hh3

message = 'this is a test message.'
print(message.split(), message.split('is'), sep='\n')
---
['this', 'is', 'a', 'test', 'message.']
['th', ' ', ' a test message.']
```



## 五、用rjust()、ljust()、center()方法对齐文本
> ljust()、rjust()、center()分别表示向左、右、中方向对其，第一个参数表示中字符串的长度，第二个参数表示填充的字符，默认是以空格填充
```
print('hello'.rjust(10))
print('hello'.ljust(10))
print('hello'.ljust(10,'*'))
print('hello'.center(10,'*'))
---
     hello
hello     
hello*****
**hello***
```


## 六、用 rstrip(),lstrip(),strip()删除字符
> rstrip(),lstrip(),strip()分别表示删除右边、左边、两边的特定字符，`默认是删除两边的空格`。
```
>>> ' hello   '.lstrip()
'hello   '
>>> '   hello   '.rstrip()
'   hello'
>>> '   hello   '.strip()
'hello'
>>> 'jjjhellojjj'.lstrip('jjj')
'hellojjj'
>>> 'jjjhellojjj'.rstrip('jjj')
'jjjhello'
>>> 'jjjhellojjj'.strip('jjj')
'hello'
```


## 七、使用pyperclip模块复制黏贴字符串

>pyperclip.copy(),pyperclip.paste()可以向计算机的剪贴板发送、接收文本
```
例子：
from pyperclip import copy, paste
copy('hhhh')
print(paste())
---
hhhh
```
## 八、字符串的替换
 >  str.replace(old, new[, max])
>参数说明：
 > -   old -- 将被替换的子字符串。
 >  - new -- 新字符串，用于替换old子字符串。
 > - max -- 可选字符串, 替换不超过 max 次
返回字符串中的 old（旧字符串） 替换成 new(新字符串)后生成的新字符串，如果指定第三个参数max，则替换不超过 max 次。
```
str = "this is string example....wow!!! this is really string"
print(str.replace("is", "was"))
print(str.replace("is", "was", 3))
---
thwas was string example....wow!!! thwas was really string
thwas was string example....wow!!! thwas is really string
```


# 第七章  模式匹配与正则表达式
>python 中所有的正则表达式的函数都在`re模块`中向 re.compile() 传入字符串值，它将返回一个Regex 模式对象。
```
常用字符分类的缩写代码

\d                 0到9的任何数字 
\D                 除0到9数字以外的任何其他字符 
\w                 任何的字母，数字，下划线(可以认为是匹配到单词字符)
\W                 除了字母、数字、下划线以外的任何字符(跟\w相反)
\s                 空格、制表符或换行符(可以认为是匹配到"空白"字符)、 
\S                 除空格，制表符和换行符以外的任何字符
```

## 一、基本模式
```
import re
numregex = re.compile(r'\d\d-\d\d')
mo = numregex.search('Test num is 45-12')
print(mo.group())
---
45-12
```
## 二、扩展
1.利用括号分组
```
import re
numregex = re.compile(r'(\d\d)-(\d\d-\d\d\d)')
mo = numregex.search('Test num is 45-12-568')
print(mo.group(1), mo.groups(), mo.group(), sep=',  ') 
a, b = mo.groups()
print(a, b, sep=',  ')
---
45,  ('45', '12-568'),  45-12-568
45,  12-568
```
>解析：mo.group(1), mo.groups(), mo.group()
通过括号进行分组，第一个括号里的是第一组，通过`group(n)`来返回；`group()`将返回所有的匹配内容，其返回的数据类型为字符串，`groups()`同样是返回所有的内容，但返回的类型是元组。

2.用管道匹配多个分组
>用管道进行匹配，在被查找的字符串中，`第一次出现的匹配文件`将会作为Match对象返回
```
>>> heroRegex = re.compile(r'Batman|Tina key')
>>> mo1 = heroRegex.search('Batman and Tina key.')
>>> mo1.group()
'Batman'
>>> mo2 = heroRegex.search('Tina key and Batman')
>>> mo2.group()
'Tina key'
# 方法mo.group()返回了完全匹配的文本'Batmobile',而mo.group(1)只是返回了第一个括号分组内匹配的文件'mobile'
>>> batRegex = re.compile(r'Bat(man|mobile|copter|bat)')
>>> mo = batRegex.search('Batmobile lost a wheel')
>>> mo.group()
'Batmobile'
>>> mo.group(1)
('mobile',)
```
3.用问号实现可选匹配

>字符？表明它前面的分组在这个模式中是可选的，可以认为"匹配这个？之前的分组零次或者一次"。
```
>>> batRegex = re.compile(r'Bat(wo)?man')
>>> mo1 = batRegex.search('The Adventures of Batman')
>>> mo1.group()
'Batman'
>>> mo2 = batRegex.search('The Adventures of Batwoman')
>>> mo2.group()
'Batwoman'
```
4.用星号匹配零次或者多次(任意次)
```
>>> batRegex = re.compile(r'Bat(wo)*man')
>>> mo1 = batRegex.search('The Adventures of Batman')
>>> mo1.group()
'Batman'
>>> mo2 = batRegex.search('The Adventures of Batwowowowowoman')
>>> mo2.group()
'Batwowowowowoman'
```
5.用加号匹配一次或多次(表示加号前面的分组必须"至少出现一次")
```
>>> batRegex = re.compile(r'Bat(wo)+man')
>>> mo1 = batRegex.search('The Adventures of Batwowoman')
>>> mo1.group()
'Batwowoman'
>>> mo2 = batRegex.search('The Adventures of Batman')
>>> mo2 == None
True
```
6.用花括号匹配特定的次数
```
# (Ha){3}      HaHaHa 表示特定的三次
# (Ha){3,5}    HaHaHa，HaHaHaHa，HaHaHaHaHa 表示一个范围，3到5次
# (Ha){3,}     表示至少三次(包括三次)
# (Ha){,3}	   表示最多三次(即0到3次)
```
```
>>> batRegex = re.compile(r'Bat(wo){3,5}man')
>>> mo1 = batRegex.search('The Adventures of Batwowoman')
>>> mo1 == None
True
>>> mo2 = batRegex.search('The Adventures of Batwowowoman')
>>> mo2.group()
'Batwowowoman'
>>> mo3 = batRegex.search('The Adventures of Batwowowowowowoman')
>>> mo3 == None
True
```
7.findall()方法
>-  默认情况下，search()将会返回第一个匹配的项，而findall()方法将会返回所有被查找字符串的匹配的项
>- findall()返回的不是一个Match对象，而是一个字符串列表
```
>>> numregex = re.compile(r'\d\d-\d\d-\d\d\d')
>>> mo = numregex.search('Test num is 45-12-568   and 12-56-456')
>>> mo.group()
'45-12-568'
>>> mo1 = numregex.findall('Test num is 45-12-568   and 12-56-456')
>>> mo1
['45-12-568', '12-56-456']
```

## 三、建立自己的字符分类
>安装\d,\w,\s等进行分类过于宽泛，因此可以通过方括号"[]"进行定义自己的字符分类，如[aeiouAEIOU]将会匹配所有的元音字母。
例如：

1.用[aeiouAEIOU]匹配元音字母
```
>>> import re
>>> voeelRegex = re.compile(r'[aeiouAEIOU]')
>>> voeelRegex.findall('RoboCop eats baby food. BABA FOOD')
['o', 'o', 'o', 'e', 'a', 'a', 'o', 'o', 'A', 'A', 'O', 'O']
###也可以使用短横表示字母或数字的范围。如，[a-zA-Z0-9]将匹配所有的大小写字母，数字。
```

2.在左方括号中插入字符"^"就可以得到非字符类，注意：在方括号内 普通的正则表达式不会被解释。如果必须要进行解释可以用“\” 进行转义
```
>>> import re
>>> voeelRegex = re.compile(r'[^aeiouAEIOU]')
>>> voeelRegex.findall('RoboCop eats baby food. BABA FOOD')
['R', 'b', 'C', 'p', ' ', 't', 's', ' ', 'b', 'b', 'y', ' ', 'f', 'd', '.', ' ',
 'B', 'B', ' ', 'F', 'D']
#得到的是非元音字母
```
## 四、以特定元素开头或结尾的匹配
>正则表达式的开始处插入符号(^)表明匹配必须发生在被查找文本的开始处。同理，符号($)则表示匹配在被查找文本的结束处。
例如：

1.以特定元素开始
```
>>> test = re.compile(r'Hello')
>>> test.findall('Hello world')
['Hello']
>>> test.search('Hello world')
<_sre.SRE_Match object; span=(0, 5), match='Hello'>
>>> test.search('hello world') == None
True
```

2.以特定元素结束
```
>>> test = re.compile(r'\d$')
>>> test.search('my num is 168')
<_sre.SRE_Match object; span=(12, 13), match='8'>
>>> test.search('my num is sixsixsix') is None
True
```
3. 用 r'^\d+$' 表示从开始到结束都是数字的字符串
```
>>> test = re.compile(r'^\d+$')
>>> test.search('123876')
<_sre.SRE_Match object; span=(0, 6), match='123876'>
>>> test.search('my num is 123876') is None
True
```
## 五、通配符
	
>在正则表达式中，"."句点字符成为“通配符”。它匹配除了换行之外的所有字符。
```
1.匹配at
>>> atRegex = re.compile(r'.at')
>>> atRegex.findall('The cat in the hat sat on the flat mat.')
['cat', 'hat', 'sat', 'lat', 'mat']

###注意：句点字符只会匹配一个字符，因此例1中的flat 只会匹配到lat 。
```

## 六、用点-星匹配所有字符(具体详见第七章 page 127)

>为了在一段文本中在某段位置匹配所有的字符串
```
例如：在一段字符串中找到名字
>>> name = re.compile(r'First name:(.*) Last name:(.*)')
>>> name.search('First name: watson Last name:wang')
<_sre.SRE_Match object; span=(0, 33), match='First name: watson Last name:wang'>
>>> name.findall('First name: watson Last name:wang')
[(' watson', 'wang')]
```

## 七、不区分大小写匹配
>若让正则表达式不区分大小写，可以向re.compile( )传入 re.IGNORECASE或者re.I 作为第二个参数
```
>>> import re
>>> test = re.compile(r'robocop',re.I)
>>> test.search('RoboCop is part man,part of machine, all cop.')
<_sre.SRE_Match object; span=(0, 7), match='RoboCop'>
```

## 八、用sub()方法替换字符串
>sub()方法需传入两个参数。第一个参数是一个字符串，用于取代发现的匹配，第二个参数是一个字符串，即正则表达式。 sub()方法返回替换完成后的字符串。
```
>>> test = re.compile(r'Agent \w+')
>>> test.sub('CENSORED','Agent Alice gave the secret documents to Agent Bob.')
'CENSORED gave the secret documents to CENSORED.'

>>> test = re.compile(r'Agent (\w)\w*') ###将Agent 及其后的一个单词替换成Agent后的一个单词的第一个字母
>>> test.sub(r'\1***','Agent Alice told Agent Carol taht Agent Eve knew Agent Bob was a double agent.')
'A*** told C*** taht E*** knew B*** was a double agent.'

```
## 九、用句点字符串匹配换行 

>传入re.DOTALL作为re.compile()的第二个参数，可以让句点字符匹配所有的字符，包括换行字符。
```
>>> test = re.compile('.*')
>>> test.search('hhhhh\njjjjj')
<_sre.SRE_Match object; span=(0, 5), match='hhhhh'>

>>> test = re.compile('.*',re.DOTALL)
>>> test.search('hhhhh\njjjjj')
<_sre.SRE_Match object; span=(0, 11), match='hhhhh\njjjjj'>	

###默认情况下，在创建时没有向re.compile()传入re.DOTALL,它将匹配所有的字符直到第一个换行符,
###但如果传入了re.DOTALL 它将匹配所有的字符。
```

# 第八章 读写文件

## #一、基础知识梳理

1. os.path.join()
```
import  os
myfiles = ['accounts.txt', 'deatils.csv', 'invite.docx']
for file in myfiles:
    print(os.path.join('C:\\Users\\scott.wang',file))

---
C:\Users\scott.wang\accounts.txt
C:\Users\scott.wang\deatils.csv
C:\Users\scott.wang\invite.docx
```

2. 当前目录，切换目录
```
>>> import os
>>> os.getcwd()   # 显示当前目录
'C:\\Users\\scott.wang'
>>> os.chdir('C:\\Users')  # 切换目录
>>> os.getcwd()
'C:\\Users'
```
3.创建新文件夹
```
>>> os.chdir(r'F:\kettle')   # 切换到kettle目录下
>>> os.listdir()  # 查看当前目录下为空
[]
>>> os.makedirs('test-dir')  # 创建test-dir 文件夹
>>> os.listdir()
['test-dir']
```
4.处理绝对路径和相对路径
```
# 将返回参数的绝对路径的字符串 
os.path.abspath(path)  
# 判断参数是不是一个绝对路径，如果是则返回True，如果是相对路径则返回false
os.path.isabs(path)   
# 将返回从start路径到path的相对路径的字符串，如果没有提供start，则默认使用当前目录作为开始路径
os.path.relpath(path,start) 
```
```
# usage of os.path.abspath()
>>> import os
>>> os.path.abspath('.')
'C:\\Users\\scott.wang'
# usage of os.path.isabs()
>>> os.path.isabs('../Users')
False
>>> os.path.isabs('C:\\Users\\scott.wang')
True
# usage of os.path.relpath()
>>> os.getcwd()
'C:\\Users\\scott.wang'
>>> os.path.relpath('c:\\windows','C:\\Users\\scott.wang')
'..\\..\\windows'
>>> os.path.relpath('c:\\windows','.')
'..\\..\\windows'
```

5.列出一个目录下的所在路径、文件/文件夹名称、剥离所在路径与文件/文件夹名称 
```
# usage of os.path.dirname()
>>> os.path.dirname(r'F:\temp\pp100-jvm-monitor.xml')
'F:\\temp'
# usage of os.path.basename()
>>> os.path.basename(r'F:\temp\pp100-jvm-monitor.xml')
'pp100-jvm-monitor.xml'
# usage of os.path.split()
>>> os.path.split(r'F:\temp\pp100-jvm-monitor.xml')
('F:\\temp', 'pp100-jvm-monitor.xml')
```


6.列出文件夹的内容以及查看文件大小
```
# usage of os.path.getsize()  and os.listdir()
>>> os.path.getsize(r'F:\temp\pp100-jvm-monitor.xml')   # 单位为字节
145910
>>> os.listdir(r'F:\temp')
['atacenter_and_web_with_sp1_x64_dvd_617598.iso', 'pp100-jvm-monitor.xml', 'pp100-
Tomcat-template.xml', 'pp100-Tomcat模板.xml', 'protocol.tar.gz']
```
7.检查路径的有效性
```
os.path.exists(path) # 判断path参数所指的文件或文件夹是否存在，存在则返回True,否则返回false
os.path.isfile(path) # 判断path参数存在并且是一个文件，如果为真返回为True，否则返回为false
os.path.isdir(path)  # 判断path参数存在并且是一个文件夹，如果为真返回为True，否则返回为false
```
8.文件的读与写

>一般而言，文件读写的三步骤：
① 调用 open()函数，返回一个File对象
② 调用File对象的 read()或者 write()方法
③ 调用File对象的 close()方法，关闭该文件


```
# usage of open file 
# method 1
a = open(r'F:\文档\部署文档\日志轮询.txt')
print(a.read())
a.close()
# method 2
with open(r'F:\文档\部署文档\日志轮询.txt') as f:
    print(f.read())

# usage of write file
## 不添加第二个参数默认是读模式，无法写；添加'w'会覆盖原有内容重新写入，需谨慎使用，'a'是追加模式，将在原有的内容后添加内容
# method 1
a = open(r'F:\文档\部署文档\日志轮询.txt', 'a')  
a.write('\nthis is test message,use to test write method of file.\n')
a.close()
# method 2 
with open(r'F:\文档\部署文档\日志轮询.txt', 'a') as f:
    f.write('\nthis is test message,use to test write method of file.\n')
```
# 第九章 组织文件

## #一、shutil模块

> **1.复制文件 shutil.copy(source,destination)**
>该函数将会返回一个字符串，表示被复制文件的路径,destination后选跟文件名，不跟文件名会使用原先的文件名。
shutil.copy2()类似于linux中的cp -p。
    destination.'''
>**2.复制文件夹 shutil.copytree(source,destination)**
该函数将会返回一个字符串，表示被复制文件夹的路径,destination一定要跟新的文件夹名，否则会有报错。
```


>>> os.chdir(r'e:\temp')
>>> os.getcwd()
'e:\\temp'
>>> os.listdir()
['des', 'dir', 'test.txt']
>>> os.listdir('dir')
['test2.txt']
>>> os.listdir('des')
[]
# usage of shutil.copy()
>>> shutil.copy(r'dir\test2.txt','des')
'des\\test2.txt'
>>> os.listdir('des')
['test2.txt']
# usage of shutil.copytree()
>>> shutil.copytree('dir',r'des\des-dir')
'des\\des-dir'
>>> os.listdir('des')
['des-dir', 'test2.txt']
```
3.文件及文件夹的移动和改名 shutil.move(source,destination)
```
# 小心目的目录下有同样的文件，如果没有改名原文件将会被覆写
>>> shutil.move(r'dir\test2.txt','des')  
'des\\test2.txt'
>>> os.listdir('dir')
[]
>>> os.listdir('des')
['des-dir', 'test2.txt']
>>> shutil.move(r'des\des-dir','dir')
'dir\\des-dir'
>>> os.listdir('des')
['test2.txt']
>>> os.listdir('dir')
['des-dir']
```
4.文件、文件夹的删除
>
>永久删除：
利用os.remove(path), os.rmdir(path) 可以删除一个文件或者空的文件夹。但利用shutil模块可以删除一个文件夹及其所有内容。
>- os.unlink(path)	 # 删除path处的文件，Remove a file (same as remove()).
>- os.rmdir(path)   # 删除path处的文件夹。该文件夹必须为空，其中没有包含任何的文件及文件夹
>- shutil.rmtree(path) # 删除path处的文件夹。它包含的所有的文件及文件夹都会被删除
安全的删除文件：使用第三方的send2trash模块


5.目录的遍历
```
a = os.walk(r'e:\temp')
for root, dirs, files in a:
    print(root)

---
e:\temp\des
e:\temp\des\des-dir
e:\temp\dir

备注：root,dirs,files 分别表示目录的结构，所有的目录名，所有的文件名
```



6.zipfile 模块
-  **创建压缩包及添加文件到压缩包**
 不能直接压缩一个文件夹，需要通过遍历的方式逐一将文件添加到文件夹中，另创建ZipFile对象时要使用'a'模式，否则会覆盖原有内容。
 
- **读取zip file**
读取zipfile首先要创建一个ZipFile对象，默认是以"读"模式打开。
- **解压文件**
ZipFile 对象的extractall()方法可以解压所有的文件及文件夹。


```
# usage of create and add files to zipfile
import os
import  zipfile
for root, dirs, files in os.walk(r'e:\temp'):
    for file in files:
        pathfile = os.path.join(root,file)
        # print(pathfile)
        test_zip = zipfile.ZipFile(r'e:\temp\test.zip','a')
        test_zip.write(pathfile)
        test_zip.close()


# usage of get information from zipfile
import os
import  zipfile
os.chdir(r'e:\temp')
testZip = zipfile.ZipFile('test.zip')  # 创建ZipFile对象
print(testZip.namelist())              # 列出压缩包里文件信息
test_info = testZip.getinfo(r'temp/test2.txt') # 创建压缩包中指定文件的ZipInfo 对象
print(test_info.file_size, test_info.compress_size) # 获取压缩文件的文件大小、压缩后的大小
testZip.close()


# usage of unzip zipfile
import os
import  zipfile
os.chdir(r'e:\temp')
test = zipfile.ZipFile('test.zip')
test.extractall(r'e:\temp')  # 解压所有的文件到temp文件夹下，如果解压指定的文件，可以使用extract()方法
test.close()
```

# 第十五章、保持时间 计划任务和启动程序
用于时间展示的两种主要模块：
- time 模块主要是用于取得Unix纪元时间戳，并加以处理。
- datetime模块可以对更方便的格式化显示日期，或对日期进行算数运算；datetime模块有自己的datetime数据类型。datetime值表示一个特定的时刻。

## #1.time模块的使用
```
>>> import time
>>> time.ctime()
'Wed Jan 17 10:52:09 2018'
>>> time.time()
1516157533.20914
>>> time.localtime()
time.struct_time(tm_year=2018, tm_mon=1, tm_mday=17, tm_hour=10, tm_min=52, tm_s
ec=19, tm_wday=2, tm_yday=17, tm_isdst=0)
>>> type(time.localtime())
<class 'time.struct_time'>
```


## #2.datetime模块的使用
```
from datetime import datetime, timedelta
# timedelta代表两个datetime之间的时间差,即表示的是时间段而非时间点
a = timedelta(days=2, hours=9)
b = timedelta(hours=10)
c = a - b
print(c.days, c.seconds/3600) # 打印c的所占用的天数，小时数
print(c.total_seconds()/3600) # 总的占用时间换算成小时数
---
1 22.0
46.0


>>> datetime.now()
datetime.datetime(2018, 1, 11, 11, 38, 24, 179910)
>>> from datetime import timedelta
>>> datetime.now() + timedelta(days=5) # 计算5天后是什么时候
datetime.datetime(2018, 1, 16, 11, 39, 5, 667283)

>>> a = datetime.strptime("2017-1-11","%Y-%m-%d")
>>> b = datetime.strptime("2017-1-15","%Y-%m-%d")
>>> a - b # a 与b之间相差多久
datetime.timedelta(-4)
>>> (a - b).days
-4


>>> import datetime
>>> delta = datetime.timedelta(days=11,hours=10,minutes=9,seconds=8)
>>> str(delta)
'11 days, 10:09:08'
>>> delta.days
11
>>> delta.seconds
36548
>>> delta.microseconds
0
>>> delta.total_seconds()
986948.0
```


## 3.datetime对象转换成字符串、字符串转化成datetime对象
- strftime() 日期格式转换成特定的字符串形式，"strftime"中的"f"表示格式，format
- strptime() 字符串格式转换为日期格式，可以将字符串格式转换为datetime 对象,"strptime"中的"p"表示解析，parse

```
# usage of strptime()
>>> from datetime import datetime
>>> test = datetime.strptime('2018-01-20',"%Y-%m-%d")
>>> test
datetime.datetime(2018, 1, 20, 0, 0)
>>> type(test)
<class 'datetime.datetime'>
>>> z = datetime.now()
>>> z
datetime.datetime(2018, 1, 11, 11, 25, 14, 747757)
>>> diff = test - z
>>> diff
datetime.timedelta(8, 45285, 252243)


# usage of strftime()
>>> datetime.datetime.now().strftime('%Y-%m-%d %H:%M:%S')
'2018-01-17 11:17:52'
>>> test = datetime.datetime.strftime(datetime.datetime.now(),'%A %B %d,%Y') # %A %B %d,%Y 分别表示完整的周几 如Monday；完整的月份；多少号；带世纪的年份 如"2018" 
>>> test
'Thursday January 11,2018'
>>> type(test)
<class 'str'>
```
#迭代器

- 概念：迭代器是一个可以记住遍历的位置的对象
- 迭代过程:迭代器对象从集合的第一个元素开始访问，直到所有的元素被访问完结束。迭代器只能往前不会后退
- 迭代器有两个基本的方法：iter() 和 next()；iter()方法用于创建一个迭代器对象，next()方法用于输出迭代器的下一个元素
- 迭代器适用对象：字符串，列表，元组

例子：
```
li = [1, 2, 3, 4]
test = iter(li)

while True:
    try:
        print(next(test))
    except StopIteration:
        print("end...")
        break

与下方执行效果一样：
print(type(test))
for x in test:
    print(x, end=' ')
---
<class 'list_iterator'>
1 2 3 4 

#备注：当next()循环完最后一个元素之后会报出“StopIteration”的错误
```
[链接：生成器详解](http://www.runoob.com/w3cnote/python-yield-used-analysis.html)

#调试
## #1.抛出异常
 抛出异常使用raise语句。在代码中，raise语句包含以下部分：
- raise关键字
- 对Exception函数的调用
- 传递给Exception函数的字符串，包含有用的出错信息

Eg：在一个长方体上打印一个字符，要求是长宽都不得小于2，字符只能是一个字符，否则就抛出异常
```
# symbol, width, height 三个参数分别是字符，宽度，长度
def BoxPrint(symbol, width, height):
    if len(symbol) != 1: 
        raise Exception("Symbol must be a single character string")
    if width <= 2:
        raise Exception("Width must be greate than 2")        # 当不满足条件时，就会报出错误
    if height <= 2:
        raise Exception("height must be greate than 2")
    print(symbol*width)    
    for i in range(height - 2):
        print(symbol + (' ' * (width - 2)) + symbol)
    print(symbol * width)


try:
    BoxPrint('#', 6, 6)
    BoxPrint('*', 1, 4) # 宽度不满足条件
except Exception as err:
    print('An exception happened: ' + str(err))

------
## #
#    #
#    #
#    #
#    #
## #
An exception happened: Width must be greate than 2
```
## #2.取得反向跟踪的字符串
如果python遇到错误，它就会生成一些错误信息，成为“反向追踪”，反向追踪包含了出错信息，导致该错误的代码行号，以及导致该错误的函数调用的序列。这个序列称为“调用栈”。利用调用栈可以帮助确定在哪次调用导致了错误。

Eg:在一个除法的计算中，我就是不想让被除数等于2，如果是就让程序报错。

```
1	def exp(n):
2	    if n == 2:
3	        raise Exception('dividend  can not be 2')
4	
5	
6	def division():
7	    x = int(input("please input a divisor:"))
8	    y = int(input("please intpu a dividend:"))
9	    exp(y)
10	    z = x / y
11	    print(z)
12	
13	
14	division()

----------
python test.py 
please input a divisor:4
please intpu a dividend:2
Traceback (most recent call last):
  File "test.py", line 12, in <module>
    division()
  File "test.py", line 8, in division
    exp(y)
  File "test.py", line 3, in exp
    raise Exception('dividend  can not be 2')
Exception: dividend  can not be 2
```
