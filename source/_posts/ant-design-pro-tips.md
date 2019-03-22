---
title: Ant Design Pro 的一些小技巧
date: 2019-03-20 15:37:04
tags: [react, ant-design]
categories: [Javascript]
---
前言：最近公司需要做一个APP的管理后台，之前公司的后台管理系统都是前后不分离的。现在考虑到后端的工作量也挺大的，所以打算前后分离了，前端我们最终决定使用蚂蚁金服开源框架：Ant Design Pro（真香）


# Tip1：怎么使用动态路由
很多公司的后台系统都是有权限控制的，所以会有动态路由这个说法，在Antd-Pro里，使用动态路由还是挺简单的：
- 找到文件src/models/menu.js
- 在effects/getMenuData里从后台拉取动态路由，再做上相应的权限控制（对menuData字段进行处理）

# Tip2： Provider和Content
- [how-does-provider-and-connect-work-in-react](https://stackoverflow.com/questions/48227188/how-does-provider-and-connect-work-in-react)
- [Context（中文）](https://zh-hans.reactjs.org/docs/context.html)
- [Higher-Order Components（中文）](https://zh-hans.reactjs.org/docs/higher-order-components.html)

# Tip3：生成动态路由
每个用户登录进来，都会根据这个人的角色加载动态的菜单和权限，但是前端的路由其实是前端在router.config.js里定义出来的静态路由，所以并不能做出动态路由。

# Tip4：权限控制
这里有几个概念需要先梳理清楚（用户、角色、权限、菜单）：
【权限】 依附于 【菜单】 依附于 【角色】 依附于 【用户】
所以应该有以下的结构：
- 用户管理 增删改查 分配角色
- 角色管理 增删改查 分配菜单和权限
- 菜单管理 增删改查
- 权限管理 增删改查

备注：权限通常都是都是依附于菜单的，但是也有两者互不联系，单独管理的情况。


