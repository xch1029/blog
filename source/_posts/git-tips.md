---
title: git无敌攻略
date: 2019-04-12 09:14:15
tags:
    - git
---

### 用户信息
配置用户个人的用户名和电子邮箱地址：
``` git
git config --global user.name "xucaihua"
git config --global user.email 158972928@qq.com
```
如果用了 --global 选项，那么更改的配置文件就是全局的，以后你所有的项目都会默认使用这里配置的用户信息。
如果要在某个特定的项目中使用其他用户字或者电子邮箱，只要去掉 --global 选项重新配置即可，新的配置保存在当前项目的 .git/config 文件里。

### 查看配置信息
要检查已有的配置信息，可以使用 git config --list 命令：
``` git
git config --list
```
也可以只查看某个变量，像这样：
``` git
git config user.name
```

### 创建仓库
Git 使用 git init 命令来初始化一个 Git 仓库，Git 的很多命令都需要在 Git 的仓库中运行，所以 git init 是使用 Git 的第一个命令：
``` git
git init
```

### 添加到暂存区和提交
初始化后，会在该目录下会出现一个名为 .git 的目录，所有 Git 需要的数据和资源都存放在这个目录中。
如果当前目录下有几个文件想要纳入版本控制，需要先用 git add 命令告诉 Git 开始对这些文件进行跟踪，然后提交：
``` git
git add *.js
git add README
git commit -m "初始化"
```
以上命令将.js结尾的文件和README提交到仓库。如果想添加全部文件，使用：
``` git
git add .
git commit -m "初始化"
```

### git clone
我们使用 git clone 从现有 Git 仓库中拷贝项目，
``` git
git clone <repo>
```
如果想指定其他目录名，而不是使用默认，使用以下命令：
``` git
git clone <repo> <directory>
```

### 查看状态
``` git
git status
```

### 缩写 add 和commit
如果你觉得 git add 提交缓存的流程太过繁琐，Git 也允许你用 -a 选项跳过这一步。命令格式如下：
``` git
git commit -am "msg"
```

### 分支管理
创建分支：
``` git
git branch (branchname)
```

切换分支：
``` git
git checkout (branchname)
```

创建并切换分支：
``` git
git checkout -b (branchname)
```

合并分支：
一旦某分支有了独立内容，你终究会希望将它合并回到你的主分支。 你可以使用以下命令将任何分支合并到当前分支中去：
``` git
git merge (branchname)
```

列出分支：
``` git
git branch
```

删除分支：
``` git
git branch -d (branchname)
```

### 查看提交历史
``` git
git log
// 单行显示
git log --oneline
// 拓扑图
git log --oneline --graph
// 倒序
git log --oneline --reverse
// 指定用户
git log --author=xucaihua --oneline -5
```

### 标签
如果你达到一个重要的阶段，并希望永远记住那个特别的提交快照，你可以使用 git tag 给它打上标签。
比如说，项目发布一个"1.0"版本。 我们可以用 git tag -a v1.0 命令给最新一次提交打上（HEAD）"v1.0"的标签。
-a 选项意为"创建一个带注解的标签"。 不用 -a 选项也可以执行的，但它不会记录这标签是啥时候打的，谁打的，也不会让你添加个标签的注解。 推荐一直创建带注解的标签。
``` git
git tag -a v1.0
```
为某次提交追加标签
``` git
git tag -a v1.0 654gfg9
```
使用git log 查看标签
``` git
git log --oneline --decorate --graph
```
查看所有标签
``` git
git tag
```

### 添加远程库
``` git
git remote add [shortname] [url]
```

例子：提交到 Github
``` git
git remote add origin git@github.com:xxx.git
git push -u origin master
```
查看当前的远程库
``` git
git remote
git remote -v
```


