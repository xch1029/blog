---
title: 操作URL的黑科技
date: 2019-06-14 18:02:06
tags: javascript
---
### 前言
现在有这么个URL：www.baidu.com/s?wd=蔡徐坤&skill=篮球&year=2019 ，怎么才能获取query上的字段呢？这时候正则表达式就派上用场了，效果如图：

![](http://pt2k23f08.bkt.clouddn.com/URLSearchParams1.jpg)

杀鸡焉用牛刀呢，今天我们来学习下专门用来处理URL的query的接口：URLSearchParams 。

### 简单使用
只需要new一个URLSearchParams的实例即可，代码：

``` javascript
let url = '?wd=蔡徐坤&skill=篮球&year=2019';
let searchParams = new URLSearchParams(url);

for (let p of searchParams) {
  console.log(p);
}
// ["wd", "蔡徐坤"]
// ["skill", "篮球"]
// ["year", "2019"]
```
### 获取单个字段
假如现在我只想获取单个字段的值，该怎么办呢？只需要调用这个实例的get方法即可， 代码：

``` javascript
searchParams.get('wd') // "蔡徐坤"
searchParams.get('skill') // "篮球"
searchParams.get('year') // "2019"
```

有时候不知道一个字段是否存在，所以想事先校验下。使用实例的has方法进行判断，代码：

``` javascript
searchParams.has('wd') // true
searchParams.has('age') // false
```

### 添加字段
实例提供了append方法来添加字段，这个方法接收两个参数，前者是key，后者是value，代码：

``` javascript
searchParams.append('age', 26);
searchParams.has('age'); // true
searchParams.get('age'); // 26
```

### 删除字段
现在不想要year字段了，直接使用delete即可，代码：

``` javascript
searchParams.delete('year');
searchParams.has('year'); // false
```

### 设置字段
有时候想重写一个字段，而不是添加(append)一个字段，这时候需要使用set方法，比如，我们觉得坤哥不仅会篮球，还会唱，跳，rap。代码：
``` javascript
searchParams.set('skill', '篮球 唱 跳 rap');
```

### 转为字符串
修改实例后，有时候需要再转为字符串，进行路由跳转等，使用toString方法

``` javascript
searchParams.toString(); // "wd=蔡徐坤&skill=篮球+唱+跳+rap&year=2019&age=26"
```

### 一波操作后

![](http://pt2k23f08.bkt.clouddn.com/URLSearchParams2.gif)

### 兼容性

现代浏览器基本没有啥大问题，但是IE的支持不是很理想。

![](http://pt2k23f08.bkt.clouddn.com/URLSearchParams3.png)

### 外链
- [MDN参考](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams)
- [博客地址查看 jser.tech](https://jser.tech/2019/06/14/操作URL的黑科技/)
- [掘金](https://juejin.im/post/5d038c9051882548ac439933)
