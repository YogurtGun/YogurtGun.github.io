---
layout: post
title: "Mac-Jekyll和github搭建个人博客"
subtitle: "搭建个人博客"
date: 2019-05-07
author: Hang
category: Blog
tags: mac-jekyll-github
finished: true
---

## 欢迎

welcome content

## 安装ruby

标题一文本

## 安装gem
mac自带, 没有则使用brew安装
```
brew install ruby
```

没有gem的参考以下网站:
https://rubygems.org/pages/download
如果安装好了gem, 建议更换为国内的源
```
# 查看源列表
gem sources -l
# 将源移除
gem sources --remove https://rubygems.org/
# 添加国内源
gem sources --add https://gems.ruby-china.org/
# 缓存
gem sources -u
```

输入gem –version查看版本号。对比下官网的版本。可以使用以下命令更新
```
sudo gem install --system

```

## 安装jekyll
```
sudo gem install jekyll
```

## 安装博客
首先需要安装bundler
```
sudo gem install bundler
```
否则会报错:
```
Dependency Error: Yikes! It looks like you don't have bundler or one of its dependencies installed
```
我还装了以下这些
```
sudo gem install jekyll-paginate
sudo gem install jekyll-gist
```
创建博客,如果没有找到jekyll命令，重启终端
```
sudo jekyll new alexblog
```
安装过程会显示一堆安装的内容，最后一行:
```
New jekyll site installed in /Users/alex/Blog/alexblog.
```

## 本地启动博客
进入到安装目录
```
cd alexblog
jekyll serve
```
输出:
```
➜  /Users/alex/Blog/alexblog jekyll serve
Configuration file: /Users/alex/Blog/alexblog/_config.yml
Configuration file: /Users/alex/Blog/alexblog/_config.yml
            Source: /Users/alex/Blog/alexblog
       Destination: /Users/alex/Blog/alexblog/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
                    done in 0.554 seconds.
 Auto-regeneration: enabled for '/Users/alex/Blog/alexblog'
Configuration file: /Users/alex/Blog/alexblog/_config.yml
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.
```
将 http://127.0.0.1:4000 复制到浏览器打开，就可以看见了。

## 异常处理
报错1:
```
xxx uninitialized constant Bundler::Plugin::API::Source xxx
```
解决1:
```
gem update --system
gem install bundler
```
报错2:
```
在执行gem install bundler的时候又报错了。查看了下, /usr/bin/bunder不存在, 而是存在/usr/local/bin/bunder
所以，用以下代码代替:
```
解决2:
```
sudo gem install -n /usr/local/bin bundle
```

## 部署到github
我的用户名为alex-my，要按照username.github.io创建一个仓库
所以，我建立了一个 YogurtGun.github.io 的仓库
得到地址
```
https://github.com/alex-my/YogurtGun.github.io.git
```
进入到本地, 将本地的内容和github尚的仓库关联
```
cd YogurtGun
git init
git add .
git commit -m "first commit"
git remote add origin https://github.com/YogurtGun/YogurtGun.github.io.git
git push -u origin master
```
注意替换为你自己的地址,在执行git push的时候，需要你输入github的账号和密码。
这个时候在浏览器上输入: YogurtGun.github.io，就可以看见博客了。

## 添加文章
参考模版: 2019-03-06-template.markdown

## 使用主题

## 绑定域名
在终端输入:
```
ping YogurtGun.github.io
```
得到ip地址:
```
PING github.map.fastly.net (xxx.xxx.xxx.xxx): 56 data bytes
```
打开域名供应商的控制台, 我这边在万网申请的com域名。
添加解析, 添加两条A记录:
```
记录类型    主机记录    解析线路(运营商)   记录值
A           @           默认              xxx.xxx.xxx.xxx
A           www         默认              xxx.xxx.xxx.xxx
```
记录值填写刚才获得的ip地址。
在博客根目录添加CNAME文件,并将你的域名写入:
```
cd YogurtGun
echo "xxx.com" > CNAME
```
将CNAME提交。待域名解析完成，就可以了。万网这边1分钟解析时间。

## Author

[Hang](https://YogurtGun.github.io)
