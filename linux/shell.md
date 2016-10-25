# SHELL #
工作形式分为两种： **交互式**，**批处理**  

查看系统中所有可用的SHELL 解释器：
<pre>
#cat /etc/shells
</pre>

查看当前的SHELL解释器：  
<pre>
#echo $SHELL
</pre>

### 编写简单的脚本 ###
Shell脚本，按照命令的执行顺序依次编写，每行一条Linux命令。  
一个完整的Shell脚本应该包括“**脚本声明**，**注释信息**和**可执行语句**”  
脚本声明（#!）:告知系统用何种shell来解释  
注释信息（#）：对可执行语句或程序功能做介绍，可以不写  
可执行语句：执行的具体命令  
示例代码，功能是显示当前的工作路径并列出当前目录的所有文件与属性
<pre>
#vim Example.sh
#!/bin/bash
#For example
pwd
ls -al
</pre>
执行脚本有三种方法：  
脚本文件路径：./Example.sh  
sh 脚本文件路径： sh Example.sh  
source 脚本文件路径： source Example.sh  
注意这样直接访问脚本文件路径方式有点特殊，  
<pre>
# ./Example.sh
-su: ./Example.sh: Permission denied
</pre>
需要为脚本设置可执行权限后，才能运行。
<pre>
#chmod u+x Example.sh
</pre>
**接收用户参数**
<pre>
$0   当前执行Shell脚本的程序名
$1-9,${10},${11}……   参数的位置变量
$#   一共有多少个参数
$*   所有位置变量的值
$?   判断上一条命令是否执行成功，0为成功，非0为失败。
</pre>
简单示例：
<pre>
#vim Example1.sh
#!/bin/bash
echo "当前脚本名称$0"
echo "总共有$#个参数，分别是$*"
echo "第一个参数是$1"
#sh Example1.sh one two three four
Name of the Program:Example1.sh
Count of Args:4,The values: one two three four
First arg: one
</pre>

**判定用户参数**
比如mkdir 命令，当目录不存在则创建，若存在则报错。  
条件测试语句能测试特定的表达式是否成立，当条件成立是返回0，否则返回其他值。  
**测试语句格式： [ 条件表达式 ]，两边均应有一个空格**  
测试语句有： 文件测试，逻辑测试，整数值比较，字符串比较。  
**文件测试： [ 操作符 文件或目录名 ]**
<pre>
-d  测试是否为目录
-e  测试文件或目录是否存在
-f  测试是否为文件
-r  测试当前用户是否有权限读取
-w  测试当前用户是否有权限写入
-x  测试当前用户是否有权限执行

root@ubuntu:~# [ -d /etc/fstab ]
root@ubuntu:~# echo $?
1
root@ubuntu:~# [ -f /etc/fstab ]
root@ubuntu:~# echo $?
0
root@ubuntu:~# [ -f /etc/fstab ] && echo $?
0
root@ubuntu:~# [ -e /dev/cdrom ] && echo "Exit"
Exit
</pre>
**逻辑测试： [ 表达式1 ] 操作符 [ 表达式2 ]**
<pre>
&&  逻辑的与，“而且”的意思
||  逻辑的或，“或者”的意思
！  逻辑的否
xiao@ubuntu:~$ [ $USER!=root ] && echo $USER
xiao
root@ubuntu:~# [ $USER!=root ] && echo $USER || echo "root"
root
</pre>
### 整数值比较： [ 整数1 操作符 整数2] ###
<pre>
-eq   判断是否等于
-ne   判断是否不等于
-gt   判断是否大于
-lt   判断是否小于
-le   判断是否小于或等于
-ge   判断是否大于或等于

</pre>

### 字符串比较： [ 字符串1 操作符 字符串2] ###
<pre>
=     比较字符串内容是否相同
！=   比较字符串内容是否不同
-z    判断字符串内容是否为空

root@ubuntu:~# echo $LANG
en_US.UTF-8
root@ubuntu:~# [ $LANG != 'en.US' ] && echo 'NOt en'
NOt en
root@ubuntu:~# [ -z $String ]
root@ubuntu:~# echo $?
0

</pre>
## 条件测试语句 ##
### if条件语句 ###
单分支结构，仅用 if then fi 关键字组成，只在条件成立后执行。  

![](http://i.imgur.com/iUuM893.jpg)

示例：判断目录是否存在，若不存在则自动创建
<pre>
#vim Example2.sh
#!/bin/bash
#For example if then fi
DIR='/home/xiao/cdrom'
if [ ! -e $DIR ]
then
mkdir -p $DIR
fi
#chmod u+x Example2.sh
#sh Example2.sh
</pre>

### 双分支if语句：由 if then else fi 组成，做条件成立或不成立的判断。
![](http://i.imgur.com/pBSRqOr.jpg)

示例：判断指定主机能否Ping通，根据返回给予提示或警告  
ping 加 -c 发送数据包个数，-i 发送数据包的间隔，-W 超过时间即超时。
<pre>
#vim Example3.sh
#!/bin/bash
ping -c 3 -i 0.2 -W 3 $1 &> /dev/null
if [ $? -eq 0 ]
then
echo "HOST $1 is up"
else
echo "HOST $1 is down"
fi
#chmod u+x Example3.sh
 chmod  u+x Example3.sh 
# source Example3.sh 
HOST  is down.
# source Example3.sh 192.168.21.1
HOST 192.168.21.1 is up.
</pre>

### 多分支结构，由 if then else elif fi 组成 ###
![](http://i.imgur.com/DoDogjX.jpg)

示例：判断用户输入的分数在哪个区间内，然后判定为 优秀，合格或不合格  
read 命令用于将用户输入参数复制给指定变量，格式为：  
<pre>
read -p [提示语句] 变量名
#vim Example4.sh
#!/bin/bash
#For if elif else
read -p "Please input score(0-100):" SCORE
if [ $SCORE -gt 100] || [ $SCORE -lt 0 ]
then
echo "Please input the right score!"
elif [ $SCORE -gt 80 ]
then
echo "Great"
elif [ $SCORE -gt 60 ]
then
echo "$SCORE"
else
echo "Bad"
fi
#chmod u+x Example4.sh
#sh Example4.sh
# sh Example4.sh 
Please input the Score:94
GREAT
# sh Example4.sh 
Please input the Score:23
BAD
# sh Example4.sh 
Please input the Score:78
COOL
# sh Example4.sh 
Please input the Score(0-100):-1
Please input the right score
# sh Example4.sh 
Please input the Score(0-100):101
Please input the right score
</pre>

### for 条件语句 ###
for 条件语句会先读取多个不同的变量值，逐一执行同一组命令
![](http://i.imgur.com/HXfr4Dj.jpg)

示例：从列表文件中读取用户名，逐一创建用户修改密码  
<pre>
# vim useradd.txt
xiao
ming
meng
# vim Example5.sh
#!/bin/bash
# example FOR 
read -p "Enter The Users PassWord:" PASSWD
for UNAME in 'cat useradd.txt'
do
id $UNAME &> /dev/null
if [ $? -eq 0 ]
echo "Already exists"
else
useradd $UNAME &> /dev/null
echo "$PASSWD\n$PASSWD" | passwd $UNAME &> /dev/null
if [ $? -eq 0 ]
then
echo "Success"
else
echo "Fail"
fi
fi
done
</pre>
