---
title: 2020年，必须拥有自己的博客网站(中)
date: 2020-02-24 12:39:27
tags: Hexo
---

在上篇教程 [2020年，必须拥有自己的博客网站(上)](https://juejin.im/post/5e514b2de51d45271849db03)中，我们使用Hexo开发了一套博客，并成功使用travis-ci将其自动化部署到github-pages，[预览地址](https://xch1029.github.io/myblog/)。

本篇教程作为这个系列的第二篇，主要讲解怎么使用Hexo进行创作以及主题的配置。

官方有个主题集合的页面[https://hexo.io/themes/](https://hexo.io/themes/)，页面上提供了大量的主题以供大家挑选。但是这不能满足所有的口味，所幸Hexo的主题配置并不局限于官方提供的这些，事实上，任何第三方主题都可以应用到你的博客上，甚至可以自定义样式，这就是Hexo在主题上的灵活性。

为了证明这点，我们并不使用来自官方页面中的主题，我们在github上找到`hexo-theme-next`主题，这个主题看起来很清爽：[地址](https://github.com/iissnan/hexo-theme-next)

### 下载主题
我们所有的主题都被放在根目录`/themes`文件夹下，现在只有一个默认主题`/themes/landscape`。我们现在将`next`主题的源码下载到`themes/next`
```
# 执行
git clone https://github.com/iissnan/hexo-theme-next.git themes/next
```

有时候，github的网速很慢，我们也可以直接打包下载，然后在themes/next中解压即可，最终你的themes目录看起来是这样的：
```
|-themes
|--landscape
|--next
```
现在主题的代码已经下载到了项目中，下一步，修改`_config.yml`文件以应用`next`主题，这个文件是`hexo`中所有配置的集合，以后我们会经常和它打交道。
```
# _config.yml
# ...
# 中文
language: zh-CN
# 应用next主题
theme: next
```
配置好后，本地启动博客：
```
hexo serve
# 或者简写 hexo s
```
完美的运行起来了。

### 主题的更新
后面，这个主题要是发布了新的版本，更新是件很简单的事儿：
```
cd themes/next
git pull
```

### 修改更多默认配置
初始化项目时有些默认的配置项不是我们想要的，我们需要再次修改`_config.yml`文件
```
# _config.yml
# ...
title: 欢迎来到德莱联盟
subtitle: '这是你歇脚的地方'
author: 迈克尔
```

![](https://user-gold-cdn.xitu.io/2020/2/24/1707762d166630c4?w=1920&h=944&f=png&s=45272)
现在有点样子了


![](https://user-gold-cdn.xitu.io/2020/2/24/170776a36206bdb1?w=640&h=133&f=png&s=4964)

页脚的强力驱动和主题我们也可以隐藏了，这些配置属于`next`，所以我们需要修改`/themes/next/_config.yml`文件
```
  powered:
    # Hexo link (Powered by Hexo).
    enable: false

  theme:
    # Theme & scheme info link (Theme - NexT.scheme).
    enable: false
```

### 开始编写第一篇文章
让我们开启创作之旅吧，写下第一篇文章。在Hexo中写作使用的是`markdown`，所以在写作之前，我们简单温习下markdown的语法：

![](https://user-gold-cdn.xitu.io/2020/2/24/1707776d5ea7a90e?w=1362&h=682&f=png&s=67550)

运行以下命令生成一篇文章
```
# hexo new [layout] <title>
hexo new welcome-lol
```
hexo自动为我们生成了.md文件：`/source/_posts/welcome-lol.md`，我们继续，开始编辑这个文件：
```
# welcome-lol.md
---
title: 欢迎大家一起来玩LOL
date: 2020-02-24 21:56:12
tags: games
---

### 什么是英雄联盟？
英雄联盟（League of Legends）是由美国Riot Games开发，腾讯游戏运营的全新英雄对战网游。英雄联盟的主创团队由各著名游戏公司的核心美术、策划、程序人员组成，他们打造了游戏中风格特色各异的英雄，加入更加丰富的物品合成系统、地图玩法、天梯匹配机制，以及独创的“召唤师”技能、符文、天赋组合，让玩家感受不一样的英雄对战网游。

在游戏中，玩家将扮演一位召唤者，并选择你所信任的联盟国进入这个游戏的正义领域，为了控制瓦罗然的权利而奋战。在这个联盟中只有一条规则：胜者就是一切！

### 全新英雄对战网游
英雄联盟中拥有的海量英雄及皮肤让人印象深刻——这些英雄不仅在外观上风格迥异，甚至个个都有自己独特的性格和脾气，例如：正气凛然的无畏先锋军团领袖—德玛西亚之力盖伦、意志坚强的弗雷尔卓德部族领袖—寒冰射手艾希、乐于钻研的魔法学者—流浪法师瑞兹……除此之外，你还可以在英雄联盟中看到代表不同地域文化特色的角色或皮肤，其中包括中国武术大师、北欧冰雪巨人、日本忍者、古埃及神话角色等。

在游戏中，身为召唤师的玩家在每局游戏中都将召唤一位英雄帮助自己进行战斗。目前已经有许多英雄协助他们达成目标，在英雄联盟中完成各自心中的正义之战！我们也深信，在英雄联盟超过100位英雄中，总有一个是合适你的！

英雄，为你而战！

注：英雄联盟每周有13位免费英雄可供使用

### 初识《英雄联盟》
首次进入游戏的玩家，系统会提示他选择自己的游戏水平，目前共分为4个等级，分别为
- 我是新手
- 我玩过英雄对战游戏
- 我是高手
- 我是大湿
> 我们强烈建议新手玩家选择等级 `我是新手` 通过游戏中的新手教程来了解基础操作。

```

![](https://user-gold-cdn.xitu.io/2020/2/24/1707784edf5b12a2?w=1920&h=944&f=png&s=74938)
真的是太酷了，hexo为我们做了大量背后的脏活，我们只要集中精力在我们的创作上即可！


### 开启更多特性
可以说，`_config.yml`文件承载着博客的一切，这一步我们加入更多的有趣特性，比如Github链接、Github徽章、关于我页面等：


![](https://user-gold-cdn.xitu.io/2020/2/24/170779b5602c481e?w=1920&h=944&f=png&s=31921)

### 提交代码
最后一步，提交代码至Github，触发travis-ci的自动化构建，再次查看我们的博客地址，已经有了新的变化！！！
[博客预览地址](https://xch1029.github.io/myblog/)

### 下一篇
请持续关注这个系列，下一篇：基于Jenkins自动化部署博客到自己的服务器和域名

