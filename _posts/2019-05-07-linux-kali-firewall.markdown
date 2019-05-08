---
layout: post
title: "kali linux 防火墙配置"
subtitle: "kali 防火墙配置"
date: 2019-05-07
author: Hang
category: Linux
tags: kali-firewall
finished: true
---

## 欢迎

welcome content

## 标题一
 Kali操作系统安装时默认已经安装了"iptables"，配置前先检查有没有安装，命令如下：iptables -L显示如下（图1），则表示已经安装了，如果没有安装，使用命令：apt-get install iptables*，带"\*"表示以"iptables"的所有相关软件包都安装，防止依赖包没有安装导致"iptables"安装失败。
 ![Codes](/img/kali_firewall/pic1.png)

 Kali iptables默认是没有任何规则配置的，允许所有的数据流通过。

**Kali iptables的规则配置语法与其它Linux版本一致，具体如下：**

（1）配置本机可以访问自身：
```
iptables -A INPUT -i lo -j ACCEPT
```

（2）配置本机可以与外部设备建立连接：
```
iptables -A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
```

（3）配置本机开放的端口，如SSH端口22：
```
iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```

（4）允许其它设备PING本机：
```
iptables -A INPUT -p icmp -j ACCEPT
```

（5）其它的INPUT规则禁止：
```
iptables -A INPUT -j REJECT --reject-with icmp-port-unreachable
```

以上只是INPUT的规则，iptables还可以配置OUTPUT、FORWARD的规则，可根据实际环境配置。

配置好规则后将保存至/etc/iptables/rules.v4，保存命令：
```
iptables-save > /etc/iptables/rules.v4
```

如果想在Kali操作系统启动时iptables设置的规则生效，则需要增加启动项：如下：

在/etc/init.d/文件夹下新建iptables文件，如：vim /etc/init.d/iptables，
内容如下：
```
#!/bin/bash
/sbin/iptables-restore < /etc/iptables/rules.v4
```

## Author

[Hang](https://YogurtGun.github.io)
