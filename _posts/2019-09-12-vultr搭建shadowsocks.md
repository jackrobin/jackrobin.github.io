---
layout: post
title: vultr搭建shadowsocks
date: 2019-09-12
catalog: true
tags:
    - shadowsocks
    - 科学上网
---
## 前言
为了实现自由畅游互联网的目的，某些时候我们需要通过一些科学的手段去上网。
## 实现方法
通过购买国外vps，搭建shadowsocks服务器，再通过客户端连接ss服务器，即可实现科学上网。
至于原理简单点说就是利用ss的加密功能，对数据进行加密，这样就可以绕过GFW屏蔽。
## 去哪里买vps？
之前有用过[搬瓦工](https://bwh1.net/index.php)，一开始稳定，高速，毕竟人家有做专门的CN线路，但是用过半年左右后，频繁出现ip被封。
搬瓦工ip被封后无法更换机房，也就无法免费更换ip，虽然有免费更新ip的策略，但是等的时间太久，要么只能花8美元更换ip，实在是贵。所以弃用了！

**所以现在用vultr**，经过2天的考察和测试，最终选择了vultr。之所以选择vultr，是因为可以免费切换ip，而且速度快，线路稳定（用了3个月没有出现问题），
当然，一个月5美元是要付的，太免费也有点假不是。

**购买注意事项**
+ 买Chicago的服务器，因为Tokyo和Singapore这些距离我们近的机房，已经被封了太多了。我当时连续换了10几个ip都被封，最后选了芝加哥的，一直非常稳定使用中
+ 操作系统我选的是Centos 7 64位
+ 然后规格就选5美元一个月的就行。25G的SSD，每个月1000G流量，基本用不完，很可以了。

*[点击购买](https://www.vultr.com/?ref=7811535)*

## 首先安装谷歌BBR（可选）
安装BBR可以优化访问速度，建议还是装下吧。
```
wget --no-check-certificate 
https://github.com/teddysun/across/raw/master/bbr.sh && chmod +x bbr.sh && ./bbr.sh
```
如果在线地址无法访问，您可以点击[脚本下载](https://nipusa.me/shell/bbr.sh)

等待成功后需要重启。重启后输入 lsmod | grep bbr ，出现 tcp_bbr 即说明 BBR 已经启动。
## 安装shadowsocks
依次执行以下命令：
```
wget — no-check-certificate -O shadowsocks.sh 
https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks.sh
```
如果在线地址无法访问，您可以点击[脚本下载](https://nipusa.me/shell/shadowsocks.sh)

```
chmod +x shadowsocks.sh
```

```
./shadowsocks.sh
```

之后会提示依次输入密码，端口，加密方式:
+ 密码：就是安装成功后客户端连接服务器的密码，设置后牢记
+ 端口：安装成功后连接服务器的端口，尽量设置大一点吧。2000以上，万一后面服务器装个啥软件，别冲突了。我设置的是2443
+ 加密方式，建议选择aes-256-cfb，因为ios和windows还是android的ss客户端，默认连接加密方式就是这个
![](https://nipusa.me/img/ss-install.png)
上面三个参数设置成功后按回车进行安装即可。
安装成功后会提示ip，端口，密码，加密方式。记好这4个信息
![](https://nipusa.me/img/ss-success.png)
接下来就可以下载客户端尝试连接服务器了。
## shadowsocks命令
**卸载：**
```
./shadowsocks.sh uninstall
```
**控制：**
```
/etc/init.d/shadowsocks start      启动
/etc/init.d/shadowsocks stop       停止
/etc/init.d/shadowsocks restart    重启
/etc/init.d/shadowsocks status     状态
```
## 客户端的使用
+ [windows客户端](https://github.com/shadowsocks/shadowsocks-windows)，里面有详细的使用介绍，也可以直接[下载](https://github.com/shadowsocks/shadowsocks-windows/releases)最新版本。
+ [android客户端](https://github.com/shadowsocks/shadowsocks-android)介绍页面，最新版本[下载](https://github.com/shadowsocks/shadowsocks-android/releases)。


**希望对您有所帮助**




