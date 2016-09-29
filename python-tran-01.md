**map()函数**，接收两个参数，一个是 函数，一个是序列。map 将传入的函数依次作用于序列的每一个元素，并把结果作为一个新的list返回。
比如把函数 f(x)=x^2 作用在一个list，[1,2,3,4]  
<pre>
def f(x):  
    return x * x  
map(f, [1,2,3,4])  
[1, 4, 9, 16]
</pre>

**reduce()函数**，接收两个参数。把一个函数作用到一个序列，这个函数必须接收两个参数，reduce把结果继续和序列的下一个元素做累积。
reduce(f, [x1,x2,x3]) = f(f(x1, x2), x3)
比如对一个序列求和。
<pre>
def add(x, y):
    return x + y
reduce(add, [1,2,3,4])
10
</pre>

练习：
把用户输入的不规范的英文名字，变为首字母大写，其他小写的规范名字。输入：['adam', 'LISA', 'barT']，输出：['Adam', 'Lisa', 'Bart']

<pre>
def test1(s):
    return str.upper(s[0]) + str.lower(s[1:])
map(test1, ['adam', 'LISA', 'barT'])

</pre>


Python提供的sum()函数可以接受一个list并求和，请编写一个prod()函数，可以接受一个list并利用reduce()求积。

<pre>
def prod(x):
    return reduce(lambda x, y: x * y, s)
prod([2, 3, 4])
</pre>