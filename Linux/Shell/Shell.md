### Shell  
Shell是一个用C语言编写的程序，它是用户使用Linux的桥梁。Shell即是一种命令语言，又是一种程序设计语言。Shell是指一种应用程序，这个程序提供了一个界面，用户通过这个界面访问操作系统内核的服务。sh是第一种Unix Shell，windows Explorer是一种典型的图形界面Shell。  
#### Shell脚本  
一种为Shell编写的脚本程序。业界所说的shell通常都是指shell脚本。但是shell和shell脚本是两个不同的概念。由于习惯原因，shell编程都是指shell脚本编程，不是指开发shell本身。  
#### Shell环境    
shell编程跟js、php一样，只要有一个文本编辑器和一个能解释执行的脚本解释器就可以了。shell种类众多，常见有：  
* Bourne Shell (/usr/bin/sh或者/bin/sh)
* Bourne Again Shell （/bin/bash)
* C Shell (/usr/bin/csh)
* K Shell (/usr/bin/ksh)
* Shell for Root(/sbin/sh)  
Bash是大多数Linux默认的Shell，一般情况下，人们不区分Bourne shell和Bourne Again Shell，所以像#!/bin/sh，它同样也可以改为#!/bin/bash。#！告诉系统其后路径所指定的程序即是解释此脚本文件的Shell程序。  
### Shell变量  
#### 1、变量定义  
```
your_name="hx.com"
```
变量名和符合之间不能有空格，同时命名必须遵守如下规则：  
* 命名只能使用英文字母，数字和下划线，首个字符不能以数字开头；
* 中间不能有空格，可以使用下划线；
* 不能使用标点符号；
* 不能使用bash里的关键字。  
#### 2、使用变量  
使用一个定义过的变量，只要在变量前面加$即可。  
```shell
your_name="abcd"
echo $your_name
echo ${your_name}
```
变量名外面的花括号是可选的，加花括号是为了帮助解析器识别变量的边界。  
已定义的变量可以被重新定义，第二次赋值时不能写$,使用变量时才加$.  
```
your_name="tom"
echo $your_name
your_name="alibaba"
echo $your_name
```
使用readonly命令可以将变量定义为只读变量，只读变量的值不能被改变。
```
#!/bin/bash
myurl="www.baidu.com"
readonly myurl
myurl="www.sina.com"
```
运行脚本会报错。  
删除变量使用unset命令。
```
unset 变量名称
```
变量被删除后不能再次使用，unset命令不能删除只读变量。   
### 变量类型  
1. 局部变量  局部变量在脚本或命令中定义，仅在当前shell实例中生效，其他shell启动的程序不能访问局部变量；  
2. 环境变量  所有的程序，包括shell的启动程序，都能访问环境变量，有些程序需要环境变量来保证其正常运行，必要的时候shell脚本也可以定义环境变量；
3. shell变量 shell变量是由shell程序设置的特殊变量，shell变量中有一部分是环境变量，有一部分是局部变量，这些变量保证了shell的正常运行。  
### Shell字符串  
字符串可以用单引号，也可以用双引号，也可以不用引号。
#### 单引号  
```
str='this is a string'
```
单引号字符串的限制：  
* 单引号里的任何字符都会原样输出，单引号字符串中的变量是无效的；
* 单引号字符串中不能出现单独一个单引号(对单引号使用转义字符也不行)，但可以成对出现，作为字符串拼接使用。  
#### 双引号  
```
your_name='tom'
str="hello,welcome \"$your_name\"! \n"
```
双引号的优点：  
* 双引号里可以有变量；
* 双引号里可以出现转义字符。  
#### 获取字符串长度  
```
string="abcd"
echo ${#string}  #输出4
```  
#### 提取子字符串  
```
string="baidu is a good site"
echo ${string:1:4} #输出aidu
```  
注意：第一字符的索引值为0。  
#### 查找字符串  
查找字符i或o的位置，(哪个字母先出现就计算那个)  
```
string="runoob is a great site"
echo `expr index "$string" io` #输出4
```
### Shell数组  
bash支持一维数组（不支持多维数组），并且没有限定数组的大小。类似C语言，数组元素下标由0开始，获取数组中的元素，下标可以是整数或算数表达式，其值应大于或等于0。  
#### 定义数组  
在Shell中，用括号来表示数据，数组元素用空格分割。  
```shell
数组名=(值1 值2 ...值n)
arry_name=(v0 v1 v2 v3)
```  
#### 读取数组  
读取数组的格式：
```
${数组名[下标]}
${arry_name[0]}
```
使用@符合可以获取数组中的所有元素  
``` shell
echo ${arry_name[@]}
```
#### 获取数组的长度
获取数组的长度与获取字符串长度的方法相同:
```shell
# 取得数组元素的个数
length=${#arry_name[@]}
#或者
leg=${#arry_name[*]}
#获取数组单个元素的长度
legt=${#arry_name[n]}
```
### Shell注释  
以#开头的行就是注释，会被解释器忽略，通过每一行加一个#设置多行注释。


