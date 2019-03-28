---
layout: post
title: "kali apt更新"
subtitle: "apt更新包"
date: 2019-03-28
author: Hang
category: Linux
tags: kali-apt
finished: true
---

## 欢迎

welcome content

## 添加更新源
```
:~# vim /etc/apt/sources.list
```
***在以下更新源中选择一个复制***
```
中科大
deb http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib
deb-src http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib

阿里云
deb http://mirrors.aliyun.com/kali kali-rolling main non-free contrib
deb-src http://mirrors.aliyun.com/kali kali-rolling main non-free contrib

清华大学
deb http://mirrors.tuna.tsinghua.edu.cn/kali kali-rolling main contrib non-free
deb-src https://mirrors.tuna.tsinghua.edu.cn/kali kali-rolling main contrib non-free

浙大
deb http://mirrors.zju.edu.cn/kali kali-rolling main contrib non-free
deb-src http://mirrors.zju.edu.cn/kali kali-rolling main contrib non-free

官方源
deb http://http.kali.org/kali kali-rolling main non-free contrib
deb-src http://http.kali.org/kali kali-rolling main non-free contrib
```

## 使用更新源进行软件升级和更新
```
:~# apt-get udpate

:~# apt-get upgrade

:~# apt-get dist-upgrade
```

## 删除旧文件和缓存文件
```
// 删除旧版本的软件缓存
:~# apt-get autoclean
// 清理所有软件缓存
:~# apt-get clean
// 删除系统不再使用的孤立软件
:~# apt-get autoremove
```

## Author

[Hang](https://YogurtGun.github.io)
