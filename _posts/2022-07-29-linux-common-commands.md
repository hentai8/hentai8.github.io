---
layout: post
---

# 查看端口占用情况

```shell
netstat  -nultp
```



# 查看硬盘io

```shell
iostat -d -k 1 10
```

 

https://blog.51cto.com/zlbzhu/758973



# 查看网络流量情况

```shell
nethogs
```





# 查看公网ip

```shell
curl ifconfig.me
curl cip.cc

```



# 查看cpu利用率

```shell
top
htop
```





# 权限

```shell
chmod 777 xxx
chmod 644 xxx
```







# 路由跟踪

```shell
tracert 47.100.40.199
```







# 查看systemctl的运行日志路径

```
cat /var/log/syslog
```





# 亚马逊扩容

查看是否可扩容

```
lsblk -f
```

扩容

```shell
sudo growpart /dev/nvme0n1 1
在以下示例中，对分区 1 上的 EXT2/EXT3/EXT4 文件系统进行扩展：

sudo resize2fs /dev/nvme0n1p1
```





# GIT









# systemctl启动程序

在这个目录下

```
/usr/lib/systemd/system
```

编辑

```shell
[Unit]
Description=pool-watcher   # 简单描述服务
After=network.target

[Service]
User=root
Group=root
WorkingDirectory=/home/ubuntu/project/pool-watcher/pool-watcher
Restart=no
ExecStart=/home/ubuntu/project/pool-watcher/pool-watcher/pool-watcher

[Install]
WantedBy=multi-user.target
```





# https自签

https://www.cnblogs.com/caidingyu/p/11904277.html

**1.key的生成** 

```
openssl genrsa -des3 -out server.key 2048
```

这样是生成rsa私钥，des3算法，openssl格式，2048位强度。server.key是密钥文件名。为了生成这样的密钥，需要一个至少四位的密码。可以通过以下方法生成没有密码的key:

```
openssl rsa -``in` `server.key -out server.key
```

server.key就是没有密码的版本了。 

**2. 生成CA的crt**

```
openssl req -new -x509 -key server.key -out ca.crt -days 3650
```

生成的ca.crt文件是用来签署下面的server.csr文件。 

**3. csr的生成方法**

```
openssl req -new -key server.key -out server.csr
```

需要依次输入国家，地区，组织，email。最重要的是有一个common name，可以写你的名字或者域名。如果为了https申请，这个必须和域名吻合，否则会引发浏览器警报。生成的csr文件交给CA签名后形成服务端自己的证书。 

**4. crt生成方法**

CSR文件必须有CA的签名才可形成证书，可将此文件发送到verisign等地方由它验证，要交一大笔钱，何不自己做CA呢。

```
openssl x509 -req -days 3650 -``in` `server.csr -CA ca.crt -CAkey server.key -CAcreateserial -out server.crt
```

输入key的密钥后，完成证书生成。-CA选项指明用于被签名的csr证书，-CAkey选项指明用于签名的密钥，-CAserial指明序列号文件，而-CAcreateserial指明文件不存在时自动生成。

最后生成了私用密钥：server.key和自己认证的SSL证书：server.crt

证书合并：

```
cat` `server.key server.crt > server.pem
```

 关于非443端口下http与https共存参考：

https://blog.51cto.com/481814/1835713

nginx配置如下

```
server {``    ``listen 442;``    ``server_name www.``test``.cn;``    ``error_page 497 https:``//``$server_name:442$request_uri; ``#正常错误反馈转换到https``    ``ssl on;``    ``ssl_certificate ..``/key/1_wx``.ltanx.cn_cert.crt;``    ``ssl_certificate_key ..``/key/2_wx``.ltanx.cn.key;``    ``ssl_protocols SSLv3 TLSv1 TLSv1.1 TLSv1.2;``    ``ssl_ciphers ALL:!ADH:!EXPORT56:RC4+RSA:+HIGH:+MEDIUM:+LOW:+SSLv2:+EXP;``    ``ssl_prefer_server_ciphers on;``    ``location ``/test/` `{``        ``proxy_pass http:``//192``.168.10.10``/test/``;``        ``proxy_redirect off;``    ``}``    ``}
```

80端口重定向到443端口，nginx配置如下

```
server {``  ``listen 80;``  ``server_name wx.ltanx.cn;``  ``rewrite ^(.*) https:``//``$server_name$1 permanent;`` ``### 使用return的效率会更高`` ``# return 301 https://$server_name$request_uri;``}
```







# pip2 python2无法使用问题

https://stackoverflow.com/questions/64187581/e-package-python-pip-has-no-installation-candidate



# 安装MySQL-python失败，即找不到MySQLdb包

https://www.codeleading.com/article/55044073039/







# Docker模式下运行falcon会导致端口探测失败



