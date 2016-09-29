# 装饰器 #
比如在函数调用前后自动打印日志，但又不修改原有函数的定义。
这种在代码运行期间动态增加功能的方式，称为：装饰器（decorator）
decorator就是一个返回函数的高阶函数。例如：
<pre>
def log(func):
    def wrapper(*args, **kw):
        print 'call %s():' % func.__name__
        return func(*args, **kw)
    return wrapper
@log
def now():
    print 'hello'
</pre>
调用now()函数，不仅会运行now()，还是会在函数前打印日志
相当于执行了 now=log(now)

如果装饰器需要传入参数，就需要编写一个返回decorator的高阶函数
比如定义log的文本：
<pre>
def log(s):
    def decorator(func):
        def wrapper(*args, **kw):
            print '%s call %s():' % (s, func.__name__)
            return func(*args, **kw)
        return wrapper
    return decorator
@log('xiao')
def now():
    print 'hello'
</pre>
相当于执行了 now=log('hello')(now)
但是。由于经过decorator装饰之后，__name__ 就已经从 now 变成了
wrapper，因为返回的函数是wrapper()，所以需要把原始函数的__name__等属性复制到wrapper()函数中，否则，有些依赖函数签名的代码会执行出错
python内置的functools.wraps就是干正事的。所以一个完整的decorator写法就如下：
![](http://i.imgur.com/yH23biR.png)    
编写一个decorator，能在函数调用的前后打印出'begin call'和'end call'的日志。    
![](http://i.imgur.com/uohRvks.png)    
能否写出一个@log的decorator，使它既支持：
<pre>@log
def f():
    pass
</pre>
又支持：
<pre>
@log('execute')
def f():
    pass
</pre>