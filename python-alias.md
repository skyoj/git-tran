# 别名 #

导入模块时，还可以使用别名，这样，可以在运行时根据当前环境选择最合适的模块。比如Python标准库一般会提供StringIO和cStringIO两个库，这两个库的接口和功能是一样的，但是cStringIO是C写的，速度更快，所以，你会经常看到这样的写法：
try:
    import cStringIO as StringIO
except ImportError: # 导入失败会捕获到ImportErrorimport StringIO
作用域

在一个模块中，我们可能会定义很多函数和变量，但有的函数和变量我们希望给别人使用，有的函数和变量我们希望仅仅在模块内部使用。在Python中，是通过_前缀来实现的。  
正常的函数和变量名是公开的（public），可以被直接引用，比如：abc，x123，PI等；  
类似\_\_xxx\_\_这样的变量是特殊变量，可以被直接引用，但是有特殊用途，比如上面的\_\_author\_\_，\_\_name\_\_就是特殊变量，hello模块定义的文档注释也可以用特殊变量\_\_doc\_\_访问，我们自己的变量一般不要用这种变量名；  
类似\_xxx和\_\_xxx这样的函数或变量就是非公开的（private），不应该被直接引用，比如\_abc，\_\_abc等；  
之所以我们说，private函数和变量“不应该”被直接引用，而不是“不能”被直接引用，是因为Python并没有一种方法可以完全限制访问private函数或变量，但是，从编程习惯上不应该引用private函数或变量。
private函数或变量不应该被别人引用，那它们有什么用呢？请看例子：
<pre>
def_private_1(name):return'Hello, %s' % name

def_private_2(name):return'Hi, %s' % name

def greeting(name):if len(name) > 3:
        return _private_1(name)
    else:
        return _private_2(name)
</pre>
我们在模块里公开greeting()函数，而把内部逻辑用private函数隐藏起来了，这样，调用greeting()函数不用关心内部的private函数细节，这也是一种非常有用的代码封装和抽象的方法，即：  
外部不需要引用的函数全部定义成private，只有外部需要引用的函数才定义为public。
