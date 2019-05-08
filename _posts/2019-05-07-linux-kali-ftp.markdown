---
layout: post
title: "kali linux FTP部署"
subtitle: "FTP部署"
date: 2019-05-07
author: Hang
category: Linux
tags: kali-ftp
finished: true
---

## 欢迎

welcome content

## 更新源列表
在安装之前需要先更新一下源列表，不然可能会导致出错,下面给出kali2.0的两个源列表:
```
sudo vim /etc/apt/sources.list
```
```
#中科大的源 - 可能有奇效：
deb http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib
#科大源
deb http://mirrors.ustc.edu.cn/kali sana main non-free contrib
deb-src http://mirrors.ustc.edu.cn/kali sana main non-free contrib
deb http://mirrors.ustc.edu.cn/kali-security sana/updates main contrib non-free

#阿里源－kali2.0较好用
deb http://mirrors.aliyun.com/kali sana main non-free contrib
deb-src http://mirrors.aliyun.com/kali sana main non-free contrib
deb http://mirrors.aliyun.com/kali-security sana/updates main contrib non-free
```
```
sudo apt-get update && apt-get upgrade
```
## 安装和配置vsftpd服务器

### 1.安装vsftpd服务器
```
sudo apt-get install vsftpd
```
查看运行状态：
```
sudo /etc/init.d/vsftpd status
```

### 2.创建专门用于上传下载的目录
```
sudo mkdir /home/uftp
sudo chmod 777 /home/uftp/　　　　#需要改变文件的读写权限，为了简单，设置成777，不然会导致无法创建文件
```

### 3.新建用户并设置密码
```
sudo useradd -d /home/uftp/ -s /bin/bash uftp
sudo passwd uftp
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

### 4.修改配置文件
```
vim /etc/vsftpd.conf
```
可以在文件开头添加以下内容:
```
userlist_deny=no
userlist_enable=yes　　　　　　　　　　
userlist_file=/etc/allowed_users　　＃允许登录的用户
seccomp_sandbox=no
```
**除此之外还需要取消下面的注释**
```
write_enable=YES　　　　#取消注释，使其生效，不然无法写入文件
```

### 5.新建/etc/allowed_users,添加允许访问的用户，我们在文件中添加我们刚才创建的用户uftp
```
vim /etc/allowed_users
uftp
```

### 6.查看文件/etc/ftpusers，文件中的列表是禁止访问用户
```
# /etc/ftpusers: list of users disallowed FTP access. See ftpusers(5).
root
daemon
bin
sys
sync
games
man
lp
mail
news
uucp
nobody
```

### 7.重启服务器vsftpd
```
sudo service vsftpd restart
或者
sudo /etc/init.d/vsftpd restart
```
到此为止，vsftpd服务器在kali上就安装完成了，下面简单演示一下如何用命令传输文件

## 用ftp命令传输文件
```
ftp ip－address
　　输入用户名和密码
put  #发送文件
　　local-file: path
　　remote-file: path
get  #接收文件
　　local-file: path
　　remote-file: path
```
## Author

[Hang](https://YogurtGun.github.io)
