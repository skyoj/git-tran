出错提示  nova list   或者 quantum agent-list 

认证出错。401

处理方式：

1, 先删除 /etc/keystone/ssl/certs 下的 index.txt文件
2: 重新  touch  index.txt
3: 重新创建 key

openssl req -key /etc/keystone/ssl/private/signing_key.pem -new -nodes -out /etc/keystone/ssl/certs/req.pem -config /etc/keystone/ssl/certs/openssl.conf -subj /C=US/ST=Unset/L=Unset/O=Unset/CN=www.example.com

openssl ca -batch -out /etc/keystone/ssl/certs/signing_cert.pem -config /etc/keystone/ssl/certs/openssl.conf -infiles /etc/keystone/ssl/certs/req.pem

4: 删除已有的 keystone-signing 文件夹。
/var/lib/nova/keystone-signing
/var/lib/quantum/keystone-signing

5: 重启 keystone  ，然后 重启 controll 的所有nova , quantum

6: 系统自动重建 keystone-signing 文件夹

7: 恢复正常。

可用 curl http://[KEYSTONE IP]:35357/v2.0/certificates/signing  查看证书的有效期。