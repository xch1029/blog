---
title: 2020年，必须拥有自己的博客网站(下)
date: 2020-02-28 17:14:11
tags: Hexo
---

一般地，我们的博客站点放在github-pages上就足矣了，所以上两篇文章中，我们着重介绍了基于travis-ci和Github来自动化部署我们的站点([上](https://juejin.im/post/5e514b2de51d45271849db03)、[中](https://juejin.im/post/5e539e4c51882549564b5623))。`零成本` + `流畅的写作体验` = `口碑爆好`！

然而，我们在愉快的创作之余，也不能忽视：即使是这么完美的方案，依旧存在一些小缺陷：
- Github站点，国内各大搜索引擎基本未收纳，也就是说你的文章很难被用户搜索到
- Github在国内的网速很慢，用户很难一直等待加载中的页面
- 在github-pages上部署的站点，域名很长，很难被用户记住

基于此，我们还有最后的大招，但涉及的知识也挺多，所以不适合新手。至少得用过点linux系统，我们先看下待会要用到的资源和技能：
- centos服务器一台
- 装上nginx、Jenkins
- 域名一个

### web hooks
我们都知道钩子的概念在前端框架中用的很多，React、Vue的生命周期都是一个一个钩子。`web hooks`和生命周期很像，只不过是换了主语和宾语，这里的主语是github，宾语是Jenkins，用图表示：

![](https://user-gold-cdn.xitu.io/2020/2/27/170870e9404111f7?w=788&h=310&f=png&s=20497)

### 需要安装的Jenkins插件
- Generic Webhook Trigger Plugin
- Publish Over SSH
- 
第一个是为了配置钩子，第二个是为了连接服务器，我们先去`Jenkins-系统配置`中将服务器配置好

![](https://user-gold-cdn.xitu.io/2020/2/27/170875e85ae93820?w=531&h=595&f=png&s=53839)

![](https://user-gold-cdn.xitu.io/2020/2/27/170875ea25179877?w=1632&h=750&f=png&s=31534)
其中的`Remote Directory`是博客构建后代码放置的位置

### 生成hooks
#### 在Jenkins的用户管理中生成Api Token

![](https://user-gold-cdn.xitu.io/2020/2/27/170874d991ea6a0a?w=465&h=916&f=png&s=64644)

![](https://user-gold-cdn.xitu.io/2020/2/27/170874dc8833ef8c?w=945&h=201&f=png&s=5925)

#### 为Github的仓库配置web hooks

![](https://user-gold-cdn.xitu.io/2020/2/27/1708752f1bf074cb?w=1505&h=782&f=png&s=54072)
URL格式为 http://<userName>:<APIToken>@<JenkinsIP>:<端口>/generic-webhook-trigger/invoke

### 配置Jenkins项目

#### 构建触发器
![](https://user-gold-cdn.xitu.io/2020/2/27/170876031729ebb0?w=1574&h=707&f=png&s=61398)
#### 选择构建环境
![](https://user-gold-cdn.xitu.io/2020/2/28/1708760b16ddd52d?w=1508&h=859&f=png&s=58249)
#### 构建脚本
![](https://user-gold-cdn.xitu.io/2020/2/28/1708760e333b2f4d?w=1190&h=354&f=png&s=9704)
#### 构建后操作
![](https://user-gold-cdn.xitu.io/2020/2/28/170876109373951a?w=1486&h=775&f=png&s=47869)

### 测试
现在，提交点代码，去Jenkins就能看到相关的构建信息了

![](https://user-gold-cdn.xitu.io/2020/2/28/17087765e0747712?w=1086&h=868&f=png&s=69502)

### Nginx
下一步就是nginx的配置，这一步相对简单
```
server {
    listen       80;
    server_name   wwww.xxxxx.com;

    location / {
        root /home/blog;
        index index.html;
    }
}
```

最后reload一下nginx即可
```
nginx -s reload
```
到这里，就可以通过自己的域名` wwww.xxxxx.com`访问博客了

### 注意
因为涉及的东西比较多，所以很多都是配了图而缺少文字解释，后面等我有时间，我再慢慢补充，慢慢解释。老铁们要是有问题或者疑问，欢迎留言，我会认真解答的！
