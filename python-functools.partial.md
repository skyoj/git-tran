# 偏函数 #
functools.partial 就是帮助我们创建一个偏函数，简单的理解就是把一个函数的某些参数给固定住（设置默认值），返回一个新的函数。更方便调用。
创建偏函数时，实际上可以接受函数对象，*args和**kw 这三个参数。
也就是说  
int2 = functools.partial(int, base=2)  
相当于 kw = {base: 2}  
max2 = functools.partial(max, 10)  
相当于 args 增加了10  
max2(5,7,6) 相当于  max(5,7,6,10)

![](http://i.imgur.com/pZqxtya.png)

当函数的参数个数太多，需要简化时，使用functools.partial可以创建一个新的函数，这个新函数可以固定住原函数的部分参数，从而在调用时更简单。