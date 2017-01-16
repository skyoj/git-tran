# windows web.py 80端口，无法创建socket #

### 80 8080 端口已经被占用,查看占用端口的PID ###，  
查看PID对应的进程。发现是 system，最后发现是win7本身的
IIS服务占用了。解决办法是，关闭 win7 的 IIS服务
<pre>
netstat -aon|findstr "80"
tasklist
</pre>
