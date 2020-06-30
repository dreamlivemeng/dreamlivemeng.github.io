---
title: github sshkey配置
date: 2020-06-29 16:03:42
categories: 
- github
tags:
- github
- sshkey
---
# github sshkey配置
## 1、创建公钥
### 1. 启动git Bash窗口
### 2.执行命令
> cd .ssh
	如果返回“… No such file or directory”，说明没有生成过SSH Key，直接进入第4步。否则进入第3步备份!
### 3.备份,也可以采用删除的模式
> mkdir key_backup mv id_isa* key_backup
### 4.生成新的key
> ssh-keygen -t rsa -C "your_email@youremail.com"
### 5.中间会让你修改路径或者输入密码短语，直接回车
### 6.提交公钥
	找到.ssh文件夹，打开id_ras.pub文件并复制里面的文本内容
	打开https://github.com/settings/ssh ,点击Add SSH Key粘贴保存就可以采用ssh模式进行克隆了
	