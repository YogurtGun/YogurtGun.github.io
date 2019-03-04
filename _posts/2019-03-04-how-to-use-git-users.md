---
layout: post
title:  如何在一电脑上配置多个Github帐号
date:   2019-03-04 17:38:00 +0800
categories: Git
tag: 教程
---

* content
{:toc}

### 1. 生成一个新的SSH key
使用 ***ssh-keygen -t rsa -C "xxx@xxx.com"*** 命令来生成新的SSH key，这里可以使用和这前一样的邮箱地址，\n
也可以使用新的邮箱地址，重要的是不能够再一直回车，要注意在提示输入文件名称时输入一个和默认名称不一样的名称，否则
会发生覆盖。 比如给文件取名叫id_rsa_6878，则会在当前文件夹中生成id_rsa_6878和id_rsa_6878.pub两个文件。

### 2.配置~/.ssh/config文件
修改~/.ssh/config文件，如果.ssh下没有这个文件可以自己创建，修改后的config文件内容如下：
```
Host github.com
    HostName github.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/id_rsa

# 第二个账号136116878
Host YogurtGun.github.com
    HostName github.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/id_rsa_6878
```
### 3.将生成的新SSH key添加到要关联的Github帐号中
我们需要将两个SSH key的密钥加入ssh 的 agent中去。我们先使用ssh-add -D将agent中的先删除，然后再依次添加。
```
1. cd ～/.ssh
2. ssh-add -D
3. ssh-add id_rsa
4. ssh-add id_rsa_6878
5. ssh-add -l
6. ssh -T git@github.com
7. ssh -T git@YogurtGun.github.com
```

### 4.使用git clone下载代码库,如果已下载请看5
要注意，在使用git clone下载代码库时，需要对地址进行修改，比如原本代码库的地址为 ***git@github.com:xxx.git***，\n
在本地使用git clone时，要改为 ***git@YogurtGun.github.com:xxx.git***。

### 5.修改 git remote
```
1. git remote -v
2. git remote rm origin
3. git remote add origin git@YogurtGun.github.com:xxx.git
```
