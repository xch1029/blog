---
title: 2020年，必须拥有自己的博客网站(上)
date: 2020-02-23 16:26:18
tags: Hexo
---
很多优秀的技术人员都有自己的博客，写博客已经成了一种习惯。作为一名程序员，你，为什么要坚持写博客？答案有很多：

- 能让人具备更好的总结能力
- 加深自己对某项技术的理解
- 获得别人的认可
- 提高自己的表达能力
- 为自己的生活留下足迹
- 证明自己的能力
- 开源精神
- 用来装逼
- ...

不管是啥理由，一个优秀的程序员都应该不断的去激励自己，在日常中检讨自己，与千万优秀人看齐，把优秀当做一直习惯。

所以，今天我们就来一步一步实现自己那独一无二的博客！

### 前言
搭建博客有很多种方案，可以从零开发所有功能([阮一峰的个人网站](http://www.ruanyifeng.com/home.html))，但这有点让人头大，繁琐的事务实在是太多了：页面的编写、后台的开发、留言板的开发。。。让人难以为继！另一种方案就是基于现有的集成框架，我们只关心自己输出的文章，其他的事情都留给框架去做。

目前，这类的框架很多：`WordPress`、`Jekyll`、`VuePress`、`Hexo`等等，都是很优秀的框架。今天，我们尝试使用`Hexo`来搭建博客。

### 初始化项目
在使用`hexo-cli`初始化项目之前，我们需要使用npm以全局安装:
```
npm install hexo-cli -g
```
初始化一个项目：
```
hexo init myblog
cd myblog
npm install
hexo server
```
因为网络的原因，加载的时间可能比较长，耐心等待下。

然后，访问[http://localhost:4000/](http://localhost:4000/)你的博客就这么跑起来了：
![](https://user-gold-cdn.xitu.io/2020/2/23/17070b5619fd2a0e?w=1380&h=1040&f=png&s=423328)

就这么跑起来了！！！很不可思议。现在有两个亟待解决的问题：

- 一：博客外观使用的是默认的`landscape`主题，太死板而且容易撞衫
- 二：我们的博客现在只是运行在本地，我们需要将之放到Github上，并且可以使用网址访问

我们先来解决**问题二**，我们迫不及待地想通过`url`来访问我们的站点了!

### 将代码托管到github上
针对国内访问`Github`网速很慢，我们也可以使用`码云`来托管代码，大体的配置都是相似的。只是个人觉得`Github`更正统一点，所以这里使用的是`Github`

要想将代码托管到`Github`上，我们需要新建一个项目：

![](https://user-gold-cdn.xitu.io/2020/2/23/17070bdd1e57eece?w=379&h=242&f=png&s=15109)

点击`New repository`按钮以新建项目：

![](https://user-gold-cdn.xitu.io/2020/2/23/17070be88f40c738?w=1181&h=851&f=png&s=59408)


填写上仓库名称和描述，然后点击`Create repository`按钮：


![](https://user-gold-cdn.xitu.io/2020/2/23/17070bff10028013?w=1329&h=802&f=png&s=69581)

看到这个页面，就代表仓库真的创建完成了，现在我们跟着红框中的步骤，将本地的源码推送到`Github`上：
```
git init
git add .
git commit -m "first commit"
git remote add origin https://github.com/xch1029/myblog.git
git push -u origin master
```

![](https://user-gold-cdn.xitu.io/2020/2/23/17070c841b7ef3f1?w=1184&h=731&f=png&s=57195)

一切顺利的话，再次访问仓库的页面，我们看到了提交的代码，这说明我们本地的源码已经`push`到了仓库里。

> 我们的目标是使用`url`来访问我们的博客，所以我们下一步使用的技术是`github-pages`，使用`github-pages`来展示我们的博客。

### 自动部署的github-pages
虽然使用的是`github-pages`，但是这并不意味着我们需要手动打包再手动部署，这一切繁杂的事务都让`travis-ci`帮我们完成吧。

> 简单介绍下`travis-ci`：`travis-ci`是一个不需要自己搭建的在线持续集成工具，其最大的特点就是能和`github`无缝衔接，而且是免费使用（针对开源项目）。使用起来也非的常容易，只需要在项目中添加`.travis.yml`配置文件

### 配置自动化部署

![](https://user-gold-cdn.xitu.io/2020/2/23/17070da9d7feecc3?w=1260&h=622&f=png&s=55151)
使用`Github`账号登录[travis](https://www.travis-ci.org/)，然后将我们的博客仓库的开关打开，这是为了告诉`travis`允许使用项目中的`.travis.yml`以自动部署。

### 编写.travis.yml
在项目的根目录中添加文件`.travis.yml`
``` yml
sudo: false
language: node_js
node_js:
  - 12 # 使用12的LTS版本
cache: npm
branches:
  only:
    - master # 只监听master分支的push
script:
  - hexo generate # 自动化构建的脚本
deploy:
  provider: pages
  skip-cleanup: true
  github-token: $GITHUB_TOKEN
  keep-history: true
  on:
    branch: master
  local-dir: public
```

注意两点：
- 一：在`_config.yml`中，第17行的root属性，需要改为和项目名字一样，这是为了保证github-pages的静态资源路径引用正确
```
# 17行改为：
root: /myblog/
```
- 二：在`.travis.yml`中我们使用了变量`$GITHUB_TOKEN`，这是`travis`能够操作`Github`的关键。我们需要在`Github`中生成一个Token，再复制到`travis`中:


![](https://user-gold-cdn.xitu.io/2020/2/23/17070f53ace8e4ca?w=861&h=298&f=png&s=23595)
    
前往Github[新建 Personal Access Token](https://github.com/settings/tokens)，只勾选 `repo` 的权限并生成一个新的 Token。Token 生成后请复制并保存好。



![](https://user-gold-cdn.xitu.io/2020/2/23/17070fe514c4b8e5?w=1507&h=187&f=png&s=10228)

回到 Travis CI，前往你的 repository 的设置页面，在 `Environment Variables` 下新建一个环境变量，Name 为 `GITHUB_TOKEN`，Value 为刚才你在 GitHub 生成的 Token。确保 `DISPLAY VALUE IN BUILD LOG` 保持不被勾选 避免你的 Token 泄漏。点击 Add 保存。

**这就是所有内容了！！！**，将我们的代码提交了，看看有没有触发`travis`的自动构建：
```
git add .
git commit -m "add travis"
git push
```

### 验证
现在访问地址：[https://xch1029.github.io/myblog](https://xch1029.github.io/myblog)，其中的`xch1029`替换成你的Github名字。

### 背后的原理
其实，travis新建了一个分支`gh-pages`以用作展示`github-pages`，而分支的内容就是我们构建后的静态资源。

![](https://user-gold-cdn.xitu.io/2020/2/23/170710a5a632be9b?w=704&h=543&f=png&s=29694)

![](https://user-gold-cdn.xitu.io/2020/2/23/170710a7bfe049b6?w=901&h=306&f=png&s=17418)

### 后续文章
因为篇幅限制（不想将文章写得太长，以免难以阅读），今天就写到这里！因为我们已经可以访问我们的博客了！

关于博文撰写、主题配置、自定义样式、自动化部署到服务器等文章，会在后续持续产出，请保持关注！





