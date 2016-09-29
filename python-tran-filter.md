**filter()** 也是接收两个参数，一个函数，一个序列。把函数作用于每一个元素。
根据返回值是True 还是 False 决定是否保留该元素
比如在一个list中删除偶数。
<pre>
def is_odd(x):
    return x % 2 == 1 
filter(is_odd, [1,2,3,4,5,6])
</pre>
**练习**

请尝试用filter()删除1~100的素数。
<pre>
def is_sushu(s):
    if isinstance(s, int):
        return 'TypeError: %s is not int !' % s
    else:
        if s == 1:
            return True
        l = [x for x in range(2, s) if s % x == 0]
        if l:
            return True
        else:
            return False
a = [x for x in range(1, 101)]
filter(is_sushu, a)
</pre>
执行结果还需检查。