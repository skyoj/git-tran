## Ubuntu 14.04 安装 openvpn ##
<pre>

$sudo apt-get install -y openvpn libssl-dev openssl
</pre>
查看版本：
<pre>
$openvpn --version

OpenVPN 2.3.2 x86_64-pc-linux-gnu [SSL (OpenSSL)] [LZO] [EPOLL] [PKCS11] [eurephia] [MH] [IPv6] built on Dec  1 2014
</pre>
查看openvpn安装产生的目录
<pre>
$dpkg -L openvpn | more

/.
/usr
/usr/share
/usr/share/man
/usr/share/man/man8
/usr/share/man/man8/openvpn.8.gz
/usr/share/doc
/usr/share/doc/openvpn
/usr/share/doc/openvpn/AUTHORS
/usr/share/doc/openvpn/COPYRIGHT.GPL.gz
/usr/share/doc/openvpn/README.auth-pam
/usr/share/doc/openvpn/PORTS
/usr/share/doc/openvpn/management-notes.txt.gz
/usr/share/doc/openvpn/examples
/usr/share/doc/openvpn/examples/sample-scripts
/usr/share/doc/openvpn/examples/sample-scripts/auth-pam.pl
/usr/share/doc/openvpn/examples/sample-scripts/ucn.pl
/usr/share/doc/openvpn/examples/sample-scripts/bridge-start
/usr/share/doc/openvpn/examples/sample-scripts/verify-cn
/usr/share/doc/openvpn/examples/sample-scripts/bridge-stop
/usr/share/doc/openvpn/examples/sample-keys
/usr/share/doc/openvpn/examples/sample-keys/pass.key
/usr/share/doc/openvpn/examples/sample-keys/pass.crt
/usr/share/doc/openvpn/examples/sample-keys/client.key
/usr/share/doc/openvpn/examples/sample-keys/ca.key
/usr/share/doc/openvpn/examples/sample-keys/README
/usr/share/doc/openvpn/examples/sample-keys/client.crt.gz
/usr/share/doc/openvpn/examples/sample-keys/ca.crt
/usr/share/doc/openvpn/examples/sample-keys/dh1024.pem
/usr/share/doc/openvpn/examples/sample-keys/server.key
/usr/share/doc/openvpn/examples/sample-keys/server.crt.gz
/usr/share/doc/openvpn/examples/sample-keys/pkcs12.p12
/usr/share/doc/openvpn/examples/sample-config-files
/usr/share/doc/openvpn/examples/sample-config-files/loopback-server
/usr/share/doc/openvpn/examples/sample-config-files/firewall.sh
/usr/share/doc/openvpn/examples/sample-config-files/server.conf.gz
/usr/share/doc/openvpn/examples/sample-config-files/openvpn-shutdown.sh
/usr/share/doc/openvpn/examples/sample-config-files/loopback-client
/usr/share/doc/openvpn/examples/sample-config-files/xinetd-client-config
/usr/share/doc/openvpn/examples/sample-config-files/static-office.conf
/usr/share/doc/openvpn/examples/sample-config-files/tls-office.conf
/usr/share/doc/openvpn/examples/sample-config-files/README
/usr/share/doc/openvpn/examples/sample-config-files/xinetd-server-config
/usr/share/doc/openvpn/examples/sample-config-files/static-home.conf
/usr/share/doc/openvpn/examples/sample-config-files/openvpn-startup.sh
/usr/share/doc/openvpn/examples/sample-config-files/tls-home.conf
/usr/share/doc/openvpn/examples/sample-config-files/office.up
/usr/share/doc/openvpn/examples/sample-config-files/home.up
/usr/share/doc/openvpn/examples/sample-config-files/client.conf
/usr/share/doc/openvpn/README.Debian.gz
/usr/share/doc/openvpn/README
/usr/share/doc/openvpn/NEWS.Debian.gz
/usr/share/doc/openvpn/changelog.Debian.gz
/usr/share/doc/openvpn/README.polarssl
/usr/share/doc/openvpn/README.IPv6
/usr/share/doc/openvpn/copyright
/usr/share/doc/openvpn/README.down-root
/usr/share/doc/openvpn/COPYING.gz
/usr/share/openvpn
/usr/share/openvpn/verify-cn
/usr/sbin
/usr/sbin/openvpn
/usr/include
/usr/include/openvpn
/usr/include/openvpn/openvpn-plugin.h
/usr/lib
/usr/lib/openvpn
/usr/lib/openvpn/openvpn-plugin-down-root.so
/usr/lib/openvpn/openvpn-plugin-auth-pam.so
/etc
/etc/bash_completion.d
/etc/bash_completion.d/openvpn
/etc/openvpn
/etc/openvpn/update-resolv-conf
/etc/network
/etc/network/if-up.d
/etc/network/if-up.d/openvpn
/etc/network/if-down.d
/etc/network/if-down.d/openvpn
/etc/init.d
/etc/init.d/openvpn
/etc/default
/etc/default/openvpn
</pre>
安装easy-rsa 用来制作openvpn相关证书
<pre>
$sudo apt-get install -y easy-rsa
$dpkg -L easy-rsa | more

/.
/usr
/usr/share
/usr/share/man
/usr/share/man/man1
/usr/share/man/man1/make-cadir.1.gz
/usr/share/easy-rsa
/usr/share/easy-rsa/openssl-1.0.0.cnf
/usr/share/easy-rsa/build-req-pass
/usr/share/easy-rsa/build-key
/usr/share/easy-rsa/inherit-inter
/usr/share/easy-rsa/sign-req
/usr/share/easy-rsa/build-key-pkcs12
/usr/share/easy-rsa/vars
/usr/share/easy-rsa/pkitool
/usr/share/easy-rsa/openssl-0.9.8.cnf
/usr/share/easy-rsa/build-dh
/usr/share/easy-rsa/build-key-pass
/usr/share/easy-rsa/revoke-full
/usr/share/easy-rsa/openssl-0.9.6.cnf
/usr/share/easy-rsa/build-ca
/usr/share/easy-rsa/build-key-server
/usr/share/easy-rsa/clean-all
/usr/share/easy-rsa/list-crl
/usr/share/easy-rsa/build-inter
/usr/share/easy-rsa/build-req
/usr/share/easy-rsa/whichopensslcnf
/usr/share/doc
/usr/share/doc/easy-rsa
/usr/share/doc/easy-rsa/README-2.0.gz
/usr/share/doc/easy-rsa/README.Debian
/usr/share/doc/easy-rsa/copyright
/usr/share/doc/easy-rsa/changelog.Debian.gz
/usr/bin
/usr/bin/make-cadir

</pre>
### 相关证书 ###
openvpn 证书分为三部分：CA证书，server端证书，Client证书
### 1、制作CA证书 ###
在/etc/openvpn目录下创建easy-rsa文件夹
<pre>
$sudo mkdir /etc/openvpn/easy-rsa/
$ll /etc/openvpn
</pre>
然后把 /usr/share/easy-rsa 目录下的所有文件复制到/etc/openvpn/ease-rsa/下
<pre>
$sudo cp -r /usr/share/easy-rsa/* /etc/openvpn/easy-rsa/
$ll /etc/openvpn/easy-rsa/
total 120
drwxr-xr-x 2 root root  4096 Oct 20 10:00 ./
drwxr-xr-x 3 root root  4096 Oct 20 09:42 ../
-rwxr-xr-x 1 root root   119 Oct 20 10:00 build-ca*
-rwxr-xr-x 1 root root   352 Oct 20 10:00 build-dh*
-rwxr-xr-x 1 root root   188 Oct 20 10:00 build-inter*
-rwxr-xr-x 1 root root   163 Oct 20 10:00 build-key*
-rwxr-xr-x 1 root root   157 Oct 20 10:00 build-key-pass*
-rwxr-xr-x 1 root root   249 Oct 20 10:00 build-key-pkcs12*
-rwxr-xr-x 1 root root   268 Oct 20 10:00 build-key-server*
-rwxr-xr-x 1 root root   213 Oct 20 10:00 build-req*
-rwxr-xr-x 1 root root   158 Oct 20 10:00 build-req-pass*
-rwxr-xr-x 1 root root   449 Oct 20 10:00 clean-all*
-rwxr-xr-x 1 root root  1471 Oct 20 10:00 inherit-inter*
-rwxr-xr-x 1 root root   302 Oct 20 10:00 list-crl*
-rw-r--r-- 1 root root  7859 Oct 20 10:00 openssl-0.9.6.cnf
-rw-r--r-- 1 root root  8416 Oct 20 10:00 openssl-0.9.8.cnf
-rw-r--r-- 1 root root  8313 Oct 20 10:00 openssl-1.0.0.cnf
-rwxr-xr-x 1 root root 13246 Oct 20 10:00 pkitool*
-rwxr-xr-x 1 root root  1035 Oct 20 10:00 revoke-full*
-rwxr-xr-x 1 root root   178 Oct 20 10:00 sign-req*
-rw-r--r-- 1 root root  2077 Oct 20 10:00 vars
-rwxr-xr-x 1 root root   740 Oct 20 10:00 whichopensslcnf*
</pre>
修改vars文件
<pre>
$sudo vi /etc/openvpn/east-rsa/vars
export KEY_COUNTRY="CN"
export KEY_PROVINCE="GD"
export KEY_CITY="ShenZhen"
export KEY_ORG="Xiao"
export KEY_EMAIL="715294035@qq.com"
export KEY_OU="Xiao"

export KEY_NAME="xiaovpn"
</pre>
vars文件主要用于设置证书的相关组织信息，红色部分的内容可以根据自己的实际情况自行修改。

其中export KEY_NAME="xiaovpn"这个要记住下，我们下面在制作Server端证书时，会使用到。
source vars命令使其生效
<pre>
#source vars
#./clean-all
</pre>
执行clean-all 会删除当前目录的keys文件夹  
正式制作CA证书
<pre>
#./build-ca
Generating a 2048 bit RSA private key
........................+++
............+++
writing new private key to 'ca.key'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [CN]:
State or Province Name (full name) [GD]:
Locality Name (eg, city) [ShenZhen]:
Organization Name (eg, company) [Xiao]:
Organizational Unit Name (eg, section) [Xiao]:
Common Name (eg, your name or your server's hostname) [Xiao CA]:
Name [xiaovpn]:
Email Address [715294035@qq.com]:
</pre>
全部回车即可。
查看keys目录
<pre>
#ll keys/

total 20
drwx------ 2 root root 4096 Oct 20 10:12 ./
drwxr-xr-x 3 root root 4096 Oct 20 10:10 ../
-rw-r--r-- 1 root root 1663 Oct 20 10:12 ca.crt
-rw------- 1 root root 1704 Oct 20 10:12 ca.key
-rw-r--r-- 1 root root    0 Oct 20 10:10 index.txt
-rw-r--r-- 1 root root    3 Oct 20 10:10 serial
</pre>
已生成 ca.crt 和 ca.key 文件。ca.crt  
把 ca.crt 文件复制到openvpn 的启动目录/etc/openvpn
<pre>
#cp keys/ca.crt /etc/openvpn/
#ll /etc/openvpn
total 20
drwxr-xr-x   3 root root 4096 Oct 20 10:22 ./
drwxr-xr-x 107 root root 4096 Oct 20 09:39 ../
-rw-r--r--   1 root root 1663 Oct 20 10:22 ca.crt
drwxr-xr-x   3 root root 4096 Oct 20 10:10 easy-rsa/
-rwxr-xr-x   1 root root 1301 Dec  2  2014 update-resolv-conf*
</pre>
### 制作server端证书 ###
<pre>
#./build-key-server xiaovpn
Generating a 2048 bit RSA private key
..................+++
................................................................+++
writing new private key to 'xiaovpn.key'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [CN]:
State or Province Name (full name) [GD]:
Locality Name (eg, city) [ShenZhen]:
Organization Name (eg, company) [Xiao]:
Organizational Unit Name (eg, section) [Xiao]:
Common Name (eg, your name or your server's hostname) [xiaovpn]:
Name [xiaovpn]:
Email Address [715294035@qq.com]:

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:Xx123456
An optional company name []:
Using configuration from /etc/openvpn/easy-rsa/openssl-1.0.0.cnf
Check that the request matches the signature
Signature ok
The Subject's Distinguished Name is as follows
countryName           :PRINTABLE:'CN'
stateOrProvinceName   :PRINTABLE:'GD'
localityName          :PRINTABLE:'ShenZhen'
organizationName      :PRINTABLE:'Xiao'
organizationalUnitName:PRINTABLE:'Xiao'
commonName            :PRINTABLE:'xiaovpn'
name                  :PRINTABLE:'xiaovpn'
emailAddress          :IA5STRING:'715294035@qq.com'
Certificate is to be certified until Oct 18 02:26:29 2026 GMT (3650 days)
Sign the certificate? [y/n]:y


1 out of 1 certificate requests certified, commit? [y/n]y
Write out database with 1 new entries
Data Base Updated
</pre>
查看生成的server端密码
<pre>
#ll keys/
total 56
drwx------ 2 root root 4096 Oct 20 10:26 ./
drwxr-xr-x 3 root root 4096 Oct 20 10:10 ../
-rw-r--r-- 1 root root 5482 Oct 20 10:26 01.pem
-rw-r--r-- 1 root root 1663 Oct 20 10:12 ca.crt
-rw------- 1 root root 1704 Oct 20 10:12 ca.key
-rw-r--r-- 1 root root  120 Oct 20 10:26 index.txt
-rw-r--r-- 1 root root   21 Oct 20 10:26 index.txt.attr
-rw-r--r-- 1 root root    0 Oct 20 10:10 index.txt.old
-rw-r--r-- 1 root root    3 Oct 20 10:26 serial
-rw-r--r-- 1 root root    3 Oct 20 10:10 serial.old
-rw-r--r-- 1 root root 5482 Oct 20 10:26 xiaovpn.crt
-rw-r--r-- 1 root root 1094 Oct 20 10:26 xiaovpn.csr
-rw------- 1 root root 1704 Oct 20 10:26 xiaovpn.key
</pre>
已生成 xiaovpn.crt xiaovpn.csr,xiaovpn.key 三件个文件。xiaovpn.crt和xiaovpn.ket是需要使用的两个文件  
再为服务器生成密钥交换文件 Diffie-Hellman
<pre>
#./build-dh
#ll keys/
total 60
drwx------ 2 root root 4096 Oct 20 10:34 ./
drwxr-xr-x 3 root root 4096 Oct 20 10:10 ../
-rw-r--r-- 1 root root 5482 Oct 20 10:26 01.pem
-rw-r--r-- 1 root root 1663 Oct 20 10:12 ca.crt
-rw------- 1 root root 1704 Oct 20 10:12 ca.key
-rw-r--r-- 1 root root  424 Oct 20 10:34 dh2048.pem
-rw-r--r-- 1 root root  120 Oct 20 10:26 index.txt
-rw-r--r-- 1 root root   21 Oct 20 10:26 index.txt.attr
-rw-r--r-- 1 root root    0 Oct 20 10:10 index.txt.old
-rw-r--r-- 1 root root    3 Oct 20 10:26 serial
-rw-r--r-- 1 root root    3 Oct 20 10:10 serial.old
-rw-r--r-- 1 root root 5482 Oct 20 10:26 xiaovpn.crt
-rw-r--r-- 1 root root 1094 Oct 20 10:26 xiaovpn.csr
-rw------- 1 root root 1704 Oct 20 10:26 xiaovpn.key
</pre>
可发现已生成 dh2048.pem文件  
把xiaovpn.crt xiaovpn.key dh2048.pem 复制到/etc/openvpn目录
<pre>
#cp keys/xiaovpn.crt keys/xiaovpn.key keys/dh2048.pem /etc/openvpn/ 
#ll /etc/openvpn
total 36
drwxr-xr-x   3 root root 4096 Oct 20 10:44 ./
drwxr-xr-x 107 root root 4096 Oct 20 09:39 ../
-rw-r--r--   1 root root 1663 Oct 20 10:22 ca.crt
-rw-r--r--   1 root root  424 Oct 20 10:44 dh2048.pem
drwxr-xr-x   3 root root 4096 Oct 20 10:10 easy-rsa/
-rwxr-xr-x   1 root root 1301 Dec  2  2014 update-resolv-conf*
-rw-r--r--   1 root root 5482 Oct 20 10:44 xiaovpn.crt
-rw-------   1 root root 1704 Oct 20 10:44 xiaovpn.key
</pre>
到此 Server端证书已经制作完成
### 制作Client证书 ###
<pre>
#./build-key xiao
#ll keys/
total 92
drwx------ 2 root root 4096 Oct 20 10:48 ./
drwxr-xr-x 3 root root 4096 Oct 20 10:10 ../
-rw-r--r-- 1 root root 5482 Oct 20 10:26 01.pem
-rw-r--r-- 1 root root 5346 Oct 20 10:48 02.pem
-rw-r--r-- 1 root root 1663 Oct 20 10:12 ca.crt
-rw------- 1 root root 1704 Oct 20 10:12 ca.key
-rw-r--r-- 1 root root  424 Oct 20 10:34 dh2048.pem
-rw-r--r-- 1 root root  237 Oct 20 10:48 index.txt
-rw-r--r-- 1 root root   21 Oct 20 10:48 index.txt.attr
-rw-r--r-- 1 root root   21 Oct 20 10:26 index.txt.attr.old
-rw-r--r-- 1 root root  120 Oct 20 10:26 index.txt.old
-rw-r--r-- 1 root root    3 Oct 20 10:48 serial
-rw-r--r-- 1 root root    3 Oct 20 10:26 serial.old
-rw-r--r-- 1 root root 5346 Oct 20 10:48 xiao.crt
-rw-r--r-- 1 root root 1058 Oct 20 10:48 xiao.csr
-rw------- 1 root root 1708 Oct 20 10:48 xiao.key
-rw-r--r-- 1 root root 5482 Oct 20 10:26 xiaovpn.crt
-rw-r--r-- 1 root root 1094 Oct 20 10:26 xiaovpn.csr
-rw------- 1 root root 1704 Oct 20 10:26 xiaovpn.key
</pre>
查看生成的证书： xiao.crt,xiao.csr和xiao.key三个文件。其中xiao.crt和xiao.key需要使用到  
到此Client证书已制作完成
### 配置Server端 ###
Server端的配置文件可以从openvpn 模板中复制并解压：
<pre>
#cp /usr/share/doc/openvpn/examples/sample-config-files/server.conf.gz /etc/openvpn/
#gzip -d server.conf.gz
#ll
total 48
drwxr-xr-x   3 root root  4096 Oct 20 10:53 ./
drwxr-xr-x 107 root root  4096 Oct 20 09:39 ../
-rw-r--r--   1 root root  1663 Oct 20 10:22 ca.crt
-rw-r--r--   1 root root   424 Oct 20 10:44 dh2048.pem
drwxr-xr-x   3 root root  4096 Oct 20 10:10 easy-rsa/
-rw-r--r--   1 root root 10289 Oct 20 10:52 server.conf
-rwxr-xr-x   1 root root  1301 Dec  2  2014 update-resolv-conf*
-rw-r--r--   1 root root  5482 Oct 20 10:44 xiaovpn.crt
-rw-------   1 root root  1704 Oct 20 10:44 xiaovpn.key
</pre>
如上图 server.conf,gzip -d 解压后删除了源文件
<pre>
#grep -vE "^#|^;|^$" server.conf
port 1194
proto tcp
dev tun
ca ca.crt
cert xiaovpn.crt
key xiaovpn.key  # This file should be kept secret
dh dh2048.pem
server 10.8.0.0 255.255.255.0
ifconfig-pool-persist ipp.txt
keepalive 10 120
comp-lzo
persist-key
persist-tun
status openvpn-status.log
verb 3
</pre>
修改UDP协议为 TCP  
修改server.csr server.key 为 xiaovpn.csr xiaovpn.key  
修改dh1024.pem 为 dh2048.pem  
如果上述文件不在 /etc/openvpn 目录下，则写相对路径  

### 启动 ###
<pre>
#/etc/init.d/openvpn start
#netstat -tunlp | grep 1194
tcp        0      0 0.0.0.0:1194            0.0.0.0:*               LISTEN      5633/openvpn
</pre>
配置Client端。
LINUX 和 windows 各有不同，但无论在什么平台都需要 Client证书和CA证书。（ca.crt , xiao.crt 和 xiao.key）  
### WINDOWS CLIENT ###
先把证书文件和client配置文件复制到 /home/xiao目录下
<pre>
#cp xiao.crt xiao.key /home/xiao/
#cp /usr/share/doc/openvpn/examples/sample-config-files/client.conf /home/xiao/
</pre>
退出 root用户，回到 xiao 的HOME 目录。使用sz命令下载这几个文件
<pre>
$sudo apt-get install lrzsz
$sz -i xiao.crt xiao.key ca.crt client.conf
</pre>
sz命令是linux同windows进行ZModem文件传输工具，优点是不用打开一个sftp工具登录后去上传下载  
sz:将选定的文件发送到本地机器  
rz:运行该命令会弹出一个文件选择窗口，从本地选择文件上传到linux服务器  
secureCRT设置默认路径:options--session options -- terminal -- Xmodem/Zmodem  
下载完毕后，修改client.conf文件并保存为 client.ovpn  
把UDP改成TCP  
把remote server 改成实际 VPN服务器地址  
把证书文件改成实际文件：   
ca ca.crt  
cert xiao.crt  
key xiao.key  
把4个文件放在同一个文件夹中，并保持 client.ovpn 唯一，  
根据服务器的OpenVPN版本，下载同样版本的客户端。  
比如2.3.2  
[下载地址](http://build.openvpn.net/downloads/releases/)  
把文件夹复制到 openvpn客户端安装的config 文件夹  
启动客户端进行连接
