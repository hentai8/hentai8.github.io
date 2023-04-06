---
layout: post
---

# Linux常用命令

# 命令行走代理

是否走代理

如果想让整个当前会话都走代理，可以直接设置环境变量：

```bash
export http_proxy=http://127.0.0.1:8889 https_proxy=http://127.0.0.1:1089
```

取消代理的环境变量：

```bash
unset http_proxy
unset https_proxy

```

# ****Ubuntu上实现多分屏窗口管理****

[https://blog.csdn.net/SiriusExplorer/article/details/103016747](https://blog.csdn.net/SiriusExplorer/article/details/103016747)

# Ubuntu 插件网站

[https://extensions.gnome.org/](https://extensions.gnome.org/)

[https://link.csdn.net/?target=https%3A%2F%2Flinux.cn%2Farticle-9447-1.html](https://link.csdn.net/?target=https%3A%2F%2Flinux.cn%2Farticle-9447-1.html)

# ubuntu 合盖不休眠

[https://www.jianshu.com/p/3fe469fc60c9](https://www.jianshu.com/p/3fe469fc60c9)

# MAC 历届默认壁纸

https://512pixels.net/projects/default-mac-wallpapers-in-5k/?ref=toolsforyou

```bash
https://512pixels.net/projects/default-mac-wallpapers-in-5k/?ref=toolsforyou
```

# rsync

```bash
rsync -avz --delete "jp1.chainweb.com::db" "/data/kda-data"

rsync --delete -azvv -e "ssh -i hentai8.pem" hentai8@18.162.116.194:/data/goerli /data/goerli
```

# **查看端口占用情况**

```bash
netstat  -nultp

# 根据pid查看占用了什么端口
netstat -natup |grep 1002579
```

# 端口抓包 ubuntu wireshark

```bash
sudo apt-get install wireshark
sudo wireshark
```

# navicat安装

[https://www.fahai.org/index.php/archives/22/](https://www.fahai.org/index.php/archives/22/)

[https://www.fahai.org/aDisk/Navicat/navicat16-premium-cs.AppImage](https://www.fahai.org/aDisk/Navicat/navicat16-premium-cs.AppImage)

# mysql8.0安装

[https://blog.51cto.com/yang/2892132](https://blog.51cto.com/yang/2892132)

```bash
# 先安装客户端，再安装服务端

sudo apt-get install mysql-client-8.0

sudo apt-get install mysql-client-core-8.0

sudo apt-get install mysql-server-8.0

# 查看密码

sudo cat /etc/mysql/debian.cnf

mysql -u debian-sys-maint -p
```

```sql
use mysql;

ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '123456';

flush privileges;
quit;
```

# postgresql安装

[https://www.postgresql.org/download/linux/ubuntu/](https://www.postgresql.org/download/linux/ubuntu/)

```bash
sudo -i -u postgres
psql
select * from xxx;
```

导入导出

[https://www.cnblogs.com/tommy-huang/p/9372160.html](https://www.cnblogs.com/tommy-huang/p/9372160.html)

# **查看硬盘io**

```bash
iostat -d -k 1 10
```

[https://blog.51cto.com/zlbzhu/758973](https://blog.51cto.com/zlbzhu/758973)

# **查看网络流量情况**

```bash
nethogs
```

# **查看公网ip**

```bash
curl ifconfig.me
curl cip.cc

```

# **查看cpu利用率**

```bash
top
htop
```

# **权限**

```bash
chmod 777 xxx
chmod 644 xxx
```

# **路由跟踪**

```bash
tracert 47.100.40.199
```

# **查看systemctl的运行日志路径**

```bash
cat /var/log/syslog
```

# **亚马逊扩容**

查看是否可扩容

```bash
lsblk -f
```

扩容

```bash
sudo growpart /dev/nvme0n1 1
# 在以下示例中，对分区 1 上的 EXT2/EXT3/EXT4 文件系统进行扩展：

sudo resize2fs /dev/nvme0n1p1
```

xfs系统的只要如下一行

```bash
sudo xfs_growfs -d
```

[https://docs.aws.amazon.com/zh_cn/AWSEC2/latest/UserGuide/ebs-using-volumes.html](https://docs.aws.amazon.com/zh_cn/AWSEC2/latest/UserGuide/ebs-using-volumes.html)

# Ubuntu22 安装搜狗输入法

[https://blog.csdn.net/Mr_Sudo/article/details/124874239](https://blog.csdn.net/Mr_Sudo/article/details/124874239)

[https://zhuanlan.zhihu.com/p/431930137](https://zhuanlan.zhihu.com/p/431930137)

# **GIT**

# **systemctl启动程序**

在这个目录下

```bash
/usr/lib/systemd/system
```

编辑

```bash
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

```bash
[Unit]
Description=ironfish-testnet1   # 简单描述服务
After=network.target

[Service]
User=root
Group=root
WorkingDirectory=/home/ubuntu/project/ironfish/ironfish-stratum/ironfish-cli
Restart=no
ExecStart=/home/ubuntu/project/ironfish/ironfish-stratum/ironfish-cli/ironfish-testnet2.sh

[Install]
WantedBy=multi-user.target
```

```bash
[Unit]
Description=aleo-pool   # 简单描述服务
After=network.target

[Service]
User=root
Group=root
WorkingDirectory=/home/ubuntu/aleo/aleo-stratum
Restart=always
ExecStart=/home/ubuntu/aleo/aleo-stratum/script.sh

[Install]
WantedBy=multi-user.target
```

**执行的sh文件最上面要加上**

**#!/bin/bash**

# 设置win+e打开文件夹快捷键

1. 添加快捷键打开主文件夹（/home）

在Ubuntu中打开主文件夹相当于在Windows中打开“我的电脑”（win+e）。配置步骤如下：

System Settings --> keyboard --> Shortcuts --> Custom Shortcuts 点击那个“+”来添加一个快捷键。

Name: Archives(可以自己定义)

Command: nautilus

点击“Apply”，我们看到快捷键已经添加，但是依然显示“Disabled”。点击那个“Disabled”,就可以输入相应的按键了。同时按住“super” "e" 即可。需要注意的是，Ubuntu中的“Super”键就是Windows中的“Windows”键，就是键盘上画着Windows四个方块标志的那个键，在键盘左下角“ctrl”键和“alt”键中间。修改好之后原来显示“Disabled”的位置显示的是新的按键组合。此时快捷键已经可以使用了，退出即可。

# **apt镜像源**

apt镜像源用中科大的

替换掉/etc/apt/sources.list

```
deb https://mirrors.ustc.edu.cn/ubuntu/ jammy main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ jammy main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ jammy-updates main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ jammy-updates main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ jammy-backports main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ jammy-backports main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ jammy-security main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ jammy-security main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ jammy-proposed main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ jammy-proposed main restricted universe multiverse
```

更新环境依赖和安装必要依赖

```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install vim gcc g++ net-tools make cmake git
```

# **cuda安装**

先安装显卡驱动 直接从右上角的Settings->About->Software Updates->Additional Drivers

安装nvidia-driver-510(不要安装带server版本的)

然后安装cuda-tool，直接用apt安装

```
sudo apt-get -y install nvidia-cuda-toolkit
```

实时查看显卡占用情况

```bash
watch -n 1 nvidia-smi
```

# **虚拟内存手动配置大小**

[https://linuxhint.com/add-swap-space-ubuntu-22-04/](https://linuxhint.com/add-swap-space-ubuntu-22-04/)

```bash
$ sudo swapon --show
$ free -h
$ df -h
$ sudo fallocate -l 1G /swapfile1
$ ls -lh /swapfile1
$ sudo chmod 600 /swapfile1
$ ls -lh /swapfile1
$ sudo mkswap /swapfile1
$ sudo swapon /swapfile1
$ sudo swapon --show
$ free -h
```

# ubuntu下安装输入法

[https://blog.csdn.net/kan2016/article/details/105735645](https://blog.csdn.net/kan2016/article/details/105735645)

# ubuntu下扩容虚拟内存

[https://www.cloudsigma.com/adding-swap-space-on-ubuntu-20-04-a-tutorial/](https://www.cloudsigma.com/adding-swap-space-on-ubuntu-20-04-a-tutorial/)

ubuntu下将idea添加到侧边栏

[https://averagelinuxuser.com/ubuntu_custom_launcher_dock/](https://averagelinuxuser.com/ubuntu_custom_launcher_dock/)

# 怎么在后台运行代码

在命令行中使用 & 符号
在 Linux 或 macOS 终端中，可以在命令行结尾加上 & 符号来让程序在后台运行。例如：

```bash
python my_program.py &
```

使用 nohup 命令
nohup 命令可以让程序在后台运行，并且即使关闭终端也不会停止运行。例如：

```bash
nohup python my_program.py &
```

使用 screen 命令
screen 命令可以让程序在一个独立的终端会话中运行，并且可以在需要的时候重新连接到该会话。例如：

```bash
screen -S my_session
python my_program.py
```

然后按下 Ctrl+A 然后按下 D 键来退出该会话。

使用 systemd 服务
在 Linux 系统中，可以使用 systemd 服务来管理后台程序。创建一个名为 my_program.service 的服务文件，然后运行以下命令：

```bash
sudo systemctl start my_program.service
```

可以在服务文件中设置程序的启动命令、环境变量等配置。

这些是常见的在后台运行代码的方式，可以根据实际情况选择最适合的方式。

# ssl证书自签

[https://zhuanlan.zhihu.com/p/196638669](https://zhuanlan.zhihu.com/p/196638669)

****Let's Encrypt****

首次创建需要在cloudflare处配置

后续更新不用配置

但是本质上是新生成了一个prikey和fullchain，还需要重新复制粘贴

```bash
sudo certbot -d *.cookiehash.org --manual --preferred-challenges dns certonly
```

# **https自签**

[https://www.cnblogs.com/caidingyu/p/11904277.html](https://www.cnblogs.com/caidingyu/p/11904277.html)

**1.key的生成**

```bash
openssl genrsa -des3 -out server.key 2048
```

这样是生成rsa私钥，des3算法，openssl格式，2048位强度。server.key是密钥文件名。为了生成这样的密钥，需要一个至少四位的密码。可以通过以下方法生成没有密码的key:

```bash
openssl rsa -``in` `server.key -out server.key
```

server.key就是没有密码的版本了。

**2. 生成CA的crt**

```bash
openssl req -new -x509 -key server.key -out ca.crt -days 3650
```

生成的ca.crt文件是用来签署下面的server.csr文件。

**3. csr的生成方法**

```bash
openssl req -new -key server.key -out server.csr
```

需要依次输入国家，地区，组织，email。最重要的是有一个common name，可以写你的名字或者域名。如果为了https申请，这个必须和域名吻合，否则会引发浏览器警报。生成的csr文件交给CA签名后形成服务端自己的证书。

**4. crt生成方法**

CSR文件必须有CA的签名才可形成证书，可将此文件发送到verisign等地方由它验证，要交一大笔钱，何不自己做CA呢。

```bash
openssl x509 -req -days 3650 -``in` `server.csr -CA ca.crt -CAkey server.key -CAcreateserial -out server.crt
```

输入key的密钥后，完成证书生成。-CA选项指明用于被签名的csr证书，-CAkey选项指明用于签名的密钥，-CAserial指明序列号文件，而-CAcreateserial指明文件不存在时自动生成。

最后生成了私用密钥：server.key和自己认证的SSL证书：server.crt

证书合并：

```
cat` `server.key server.crt > server.pem
```

关于非443端口下http与https共存参考：

[https://blog.51cto.com/481814/1835713](https://blog.51cto.com/481814/1835713)

nginx配置如下

```
server {``    ``listen 442;``    ``server_name www.``test``.cn;``    ``error_page 497 https:``//``$server_name:442$request_uri; ``#正常错误反馈转换到https``    ``ssl on;``    ``ssl_certificate ..``/key/1_wx``.ltanx.cn_cert.crt;``    ``ssl_certificate_key ..``/key/2_wx``.ltanx.cn.key;``    ``ssl_protocols SSLv3 TLSv1 TLSv1.1 TLSv1.2;``    ``ssl_ciphers ALL:!ADH:!EXPORT56:RC4+RSA:+HIGH:+MEDIUM:+LOW:+SSLv2:+EXP;``    ``ssl_prefer_server_ciphers on;``    ``location ``/test/` `{``        ``proxy_pass http:``//192``.168.10.10``/test/``;``        ``proxy_redirect off;``    ``}``    ``}
```

80端口重定向到443端口，nginx配置如下

```
server {``  ``listen 80;``  ``server_name wx.ltanx.cn;``  ``rewrite ^(.*) https:``//``$server_name$1 permanent;`` ``### 使用return的效率会更高`` ``# return 301 https://$server_name$request_uri;``}
```

# **pip2 python2无法使用问题**

[https://stackoverflow.com/questions/64187581/e-package-python-pip-has-no-installation-candidate](https://stackoverflow.com/questions/64187581/e-package-python-pip-has-no-installation-candidate)

# **安装MySQL-python失败，即找不到MySQLdb包**

[https://www.codeleading.com/article/55044073039/](https://www.codeleading.com/article/55044073039/)

# **Docker模式下运行falcon会导致端口探测失败**

# 使用goland编译器，对于单词拼写检查的字典设置，怎么让其跟随项目

GoLand 编译器使用的单词拼写检查字典是基于系统设置的，因此您需要在系统设置中进行更改，以便让其跟随项目。以下是在 Mac 操作系统上更改单词拼写检查字典的步骤：

1. 打开 GoLand 编译器，并点击菜单栏中的 "GoLand" 选项。
2. 选择 "Preferences"。
3. 在 "Preferences" 窗口中，选择 "Editor" 选项卡。
4. 点击 "Spelling" 选项卡，您将看到 "Dictionaries" 选项卡。
5. 在 "Dictionaries" 选项卡中，点击 "+ " 按钮以添加新的字典。
6. 在弹出的对话框中，选择 "Custom" 并为字典命名。接下来，选择您想要使用的字典文件（可以是 .dic 或 .txt 文件）并点击 "OK"。
7. 现在您将看到新的字典已添加到列表中。将其设置为默认字典，并将 "Project" 选项卡设置为 "Use"，以便它将跟随项目。
8. 点击 "Apply" 和 "OK"，保存更改并关闭 "Preferences" 窗口。

现在，GoLand 编译器将使用您选择的自定义字典，并在您打开项目时自动加载它。如果您的项目使用其他语言或单词拼写检查字典，请重复以上步骤并添加相应的字典。

# 统计项目中每个人贡献的行数

```bash
git log --author="lu" --pretty=tformat: --numstat | gawk '{ add += $1 ; subs += $2 ; loc += $1 - $2 } END { printf "增加的行数:%s 删除的行数:%s 总行数: %s\n",add,subs,loc }'
```

# RAID5的不安全性

[https://www.zhihu.com/question/20164654/answer/348274179](https://www.zhihu.com/question/20164654/answer/348274179)

# 前后台开发总结

后台的报错要尽可能详细，前台的报错要尽可能模糊