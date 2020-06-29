---
title: hexo+github 个人博客搭建之旅
date: 2020-06-29 16:03:42
categories: 
- web前端
tags:
- hexo
- hexo+github
- 个人博客
---
# hexo+github 个人博客搭建之旅
> 本次搭建博客采用了hexo+github的方式去搭建，记录踩过的坑，避免朋友们再次踩相同的坑。
## 1、配置需要的环境(基于windows系统)
	安装git, [下载git](https://git-scm.com/)
	安装node.js,[下载node.js]https://nodejs.org/en/ 
## 2、搭建hexo环境
### 1.安装Hexo
	打开cmd命令输入以下命令
	`npm install -g hexo-cli`
	cmd命令进入指定盘符的文件夹进行hexo初始化
	`hexo init Test`
	进入test目录，安装npm环境
	`npm install`
	依次输入命令进行hexo生成
	`hexo g`
	`hexo s`
	本地就生成了可访问的博客地址,默认为localhost:4000，Ctrl+C可停止服务的运行
## 3、更换博客主题模板并发布到github
### 1.创建github仓库
		Repository name为博客地址,github博客地址仓库前缀需要与Owner一致，比如我的owner是dreamlivemeng，那么我的博客地址为dreamlivemeng.github.io
### 2.切换主题
		hexo博客很多大佬提供了非常好的主题，我的主题是hexo-theme-indigo，首先克隆下来主题
		`git clone https://github.com/yscoder/hexo-theme-indigo.git`
		把克隆下来的内容拷贝到Test/theme下面，不同的主题下面都有_config.yml可以进行配置
		然后找到Test目录下找到_config.yml进行配置
		修改主题名字为: hexo-theme-indigo,需要注意冒号后面有一个空格
		`theme: hexo-theme-indigo-card`
### 3.关联github地址
		然后找到Test目录下找到_config.yml进行配置
		```
			type: git
			repository: git@github.com:dreamlivemeng/dreamlivemeng.github.io.git 
			branch: master
		```
		这些字段默认都是有的只需要找到该后面的值
### 4.博客生成以及发布到github
		`npm install hexo-deployer-git --save`
		继续用命令生成博客
		`hexo g`
		发布到git
		`hexo d`
		这个时候就可以通过网址访问博客了dreamlivemeng.github.io
### 4、生成标签以及分类
#### 1.生成标签
		打开cmd命令行，进入博客所在文件夹，执行命令
		`hexo new page tags`
		这个时候会在对应目录生成source/tags/index.md,打开进行编辑
		```
		---
		title: tags
		date: 2020-06-29 14:05:53
		layout: "tags"
		---
		```
#### 2.生成分类
		打开cmd命令行，进入博客所在文件夹，执行命令
		`hexo new page categories`
		这个时候会在对应目录生成source/categories/index.md,打开进行编辑
		```
		---
		title: categories
		date: 2020-06-29 14:05:53
		layout: "categories"
		---
		```
#### 2.跟文章增加分类和标签
		打开需要编辑的博客文件md文件,
		```
		---
		title: Hexo博客+Github博客教程：03添加分类，标签
		date: 2018-11-01 14:17:46
		categories: 
			- 基础知识
			- hexo
		tags:
			- hexo
			- github
			- 博客
		---
		```
		需要注意的是tags和categories下面对应的标签和类别需要空格的

### 5、更换电脑怎么继续生成博客
> 网站的部署其实就是生成静态文件，hexo下所有生成的静态文件会放在public/文件夹中，所谓部署deploy其实就是将public/文件夹中内容上传到git仓库heimu24.github.io中。也就是说，你的仓库heimu24.github.io中的文件只是blog（或者命名为hexo）文件夹下的public/下的文件
#### 1.建立github的分支来保存生成博客所需要的内容
		在本地某文件夹右键git bash here,将自己的项目克隆到本地
		git clone git@github.com:dreamlivemeng/dreamlivemeng.github.io.git
		然后会生成一个文件夹dreamlivemeng.github.io,删除文件夹中除了.git的其他所有文件夹
		把你的blog文件夹内的所有文件全部复制到dreamlivemeng.github.io下
		创建忽略文件.gitignore,有就无须创建
		```
			.DS_Store
			Thumbs.db
			db.json
			*.log
			node_modules/
			public/
			.deploy*/
		```
		创建分支
		`git checkout -b hexo`
		添加所有文件到暂存区
		`git add --all`
		进行提交
		`git commit -m ""`
		推送hexo分支到github仓库
		`git push --set-upstrem origin hexo`
#### 2.新电脑中去配置文件并发布
		打开任意文件进行克隆
		`git clone -b hexo git@github.com:dreamlivemeng/dreamlivemeng.github.io.git`
		根据提示可能需要安装hexo或者是npm
		`npm install`
		这样环境就配置好了就可以继续写博客发布博客了
##### 3.写博客以及备份环境
		在source/_posts目录下创建md文件并写博客
		通过命令发布博客
		`hexo g`
		`hexo d`
		git命令提交代码
		`git add . -A`
		`git commit -m "注释"`
		`git pull --rebase`
		`git push origin hexo`
		