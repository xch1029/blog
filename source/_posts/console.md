---
title: console完全指北
date: 2020-03-13 18:14:11
tags: Javascript
---

一直以来，作为前端工程师，调试bug的时候，用的最多的就是`console.log`，我是中枪了，哈哈。其实，console还有很多不为人知的功能和一些新奇的玩法。比如下图是知乎的控制台打印内容：

![](https://user-gold-cdn.xitu.io/2020/3/13/170d2224b0ff2ad0?w=942&h=352&f=png&s=17190)

逼格一下子就上来了，有没有？


### 开始之前，看清对象
不要误会，这里的对象不是你的女朋友哦，在开始学习console之前，我们打印下console本身，看看它到底长什么样
```
console.log(console)
```

![](https://user-gold-cdn.xitu.io/2020/3/13/170d229aef30615e?w=527&h=494&f=png&s=24360)

大概长这样，一个庞然大物，不要担心，接下来，我们来解剖下对象

### 第一个命令：清空
我们习惯了在调试之前清空下控制台，保持整洁。常见的做法就是点击控制台提供的清空按钮。在这：

![](https://user-gold-cdn.xitu.io/2020/3/13/170d22d6c2b8904e?w=787&h=337&f=png&s=17740)

同时，我们可以调用console对象的clear方法达到同样的效果：

```
console.clear()
```
执行后提示`console was cleared`，就代表清空啦

![](https://user-gold-cdn.xitu.io/2020/3/13/170d22f857cfce9f?w=360&h=146&f=png&s=3216)

### 高频指令
有几个使用频率非常高的指令：
```
console.log()
consle.warn()
console.error()
```
#### console.log
`conosle.log`是我们最常用的指令，没有之一，我以前一直以为控制台只有这么一个功能，哈哈。
##### 单参数
```
// 1.字符串
console.log('在别的游戏里，像我这么帅的一般都是主角哦！')
// 2.数字
console.log(100)
// 3.对象
console.log({object: '对象'})
// 4.数组
console.log(['array', '数组'])
```

![](https://user-gold-cdn.xitu.io/2020/3/13/170d239aa20bf1be?w=429&h=213&f=png&s=8920)

##### 多参数
`console.log()`可以接受多个参数：
```
console.log('Noxians… I hate those guys', '在别的游戏里，像我这么帅的一般都是主角哦！')
console.log(100, 200)
console.log({object: '对象1'}, {object: '对象2'})
console.log(['array', '数组1'], ['array', '数组2'])
```

![](https://user-gold-cdn.xitu.io/2020/3/13/170d23db82f33079?w=598&h=150&f=png&s=11342)

##### 替换模式
`console.log`支持字符串替换模式：
```
console.log('%s很生气，后果很严重！', '俺')
console.log('是的，只要%i，就能让你爽到不能呼吸', 998)
console.log('这是你的对象: %o', {object: '对象'})
```

![](https://user-gold-cdn.xitu.io/2020/3/13/170d2447bd55c902?w=436&h=114&f=png&s=6887)

##### 样式
可以为打印出来的文字应用`css`样式，这个功能着实厉害，玩得好可以大秀逼格，先看个简单的例子：
```
console.log('%c我还以为你从来都不会选我呢', 'color: red; font-size: 30px')
```

![](https://user-gold-cdn.xitu.io/2020/3/13/170d2ecc9c97210a?w=538&h=67&f=png&s=9100)

还可以配置多处的样式：
```
console.log('你们知道最强的%c武器%c是什么？没错，就是%c补丁', 'color: blue;', '', 'color: yellow;font-size: 30px')
```

![](https://user-gold-cdn.xitu.io/2020/3/13/170d2f02b6b228c0?w=805&h=68&f=png&s=5472)
是不是很香！但是这也有个小问题，样式越写越多，阅读起来很麻烦，接下来看下更高级的用法：
```
console.log('%c大部分人都会打飞机，这对飞机来说很不公平！', `
  background: white;
  border: 3px solid red;
  border-radius: 10px;
  color: red;
  font-size: 50px;
  margin: 40px;
  padding: 20px;
  box-shadow: 0 2px 3px 0 rgba(0,0,0,.05);
`);
```


![](https://user-gold-cdn.xitu.io/2020/3/13/170d2f7990302658?w=1265&h=344&f=png&s=27500)

这个高级用法惊艳到你了吗？发挥你的想象力，可以打印出各种骚东西的！

这种行内样式写起来可能有点冗长，我们还可以使用变量来维护样式：
```
const clearStyles = '';
const largeText = 'font-size: 20px;';
const yellowText = 'color: yellow;';
const largeRedText = 'font-size: 20px; color: red;';
const largeGreenText = 'font-size: 20px; color: green;';

console.log(`%c说教无益，%c折断的 %c骨头%c才是更好的%c课本`,
  largeRedText,
  clearStyles,
  largeGreenText,
  clearStyles,
  largeText + yellowText
);
```

![](https://user-gold-cdn.xitu.io/2020/3/13/170d2ff74ed7e524?w=550&h=222&f=png&s=14589)

#### console.warn
`console.warn`的警告等级比log高点，有些插件库里会这么用：
```
console.warn('componentWillReceiveProps已经过时了，请及时迁移，我们将在下个版本移除')
```

![](https://user-gold-cdn.xitu.io/2020/3/13/170d30806a4d23ce?w=761&h=46&f=png&s=4907)

#### console.error
`console.error`级别最高，已经阻塞代码了，样式上也更加显眼：
```
console.error('Uncaught ReferenceError: girlFriend is not defined')
```

![](https://user-gold-cdn.xitu.io/2020/3/13/170d309a6b53f74a?w=574&h=46&f=png&s=3864)

### 断言 assert
`console.assert`和`console.error`有点接近，但是assert由判断条件来决定是否打印：
```
let age = 17
console.assert(age > 18, '未成年禁止观看')
```

![](https://user-gold-cdn.xitu.io/2020/3/13/170d31105f2b3dd9?w=475&h=57&f=png&s=3336)

### 技术 count
有时候想知道某个函数在某段时间内被调用了多少次，这时候可以使用`console.count`，很简单的语法：
```
console.count()
// default: 1
console.count()
// default: 2
console.count()
// default: 3
```
也可以传入一个参数作为label，替换掉默认的default：
```
console.count('函数一被调用了')
// 函数一被调用了: 1
console.count('函数一被调用了')
// 函数一被调用了: 2
console.count('函数一被调用了')
// 函数一被调用了: 3
```
另外`console.countReset()`可以重置计数，用的频率就更少了，可以忽略

### 成组 group groupEnd
```
// 一般使用
console.group()
console.log('欢迎来到')
console.log('德莱联盟')
console.groupEnd()
// 带标题
console.group('德莱文')
console.log('欢迎来到')
console.log('德莱联盟')
console.groupEnd()
// 标题带样式
console.group('%c德莱文', 'font-size: 20px;color: blue;')
console.log('欢迎来到')
console.log('德莱联盟')
console.groupEnd()
```

![](https://user-gold-cdn.xitu.io/2020/3/13/170d329bc1367d3e?w=268&h=196&f=png&s=4808)

### 表格模式 table
`console.table`会将打印的数组或者对象以表格的形式展示：
```
let name = ['英', '雄', '联', '盟']
console.table(name)

let heroInfo = {
    name: '小炮',
    age: 13,
    say: '我好想射点儿什么！'
}
console.table(heroInfo)
```

![](https://user-gold-cdn.xitu.io/2020/3/13/170d32feae83c20a?w=743&h=260&f=png&s=7485)
打印出来的数据看起来还是很舒服的，数组的index是0,1,2...，对象的index是自己的keys。
那么打印`对象数组`是什么展示方式呢：
```
let heroList = [
    {
        name: '小炮',
        age: 13,
        say: '我好想射点儿什么！'
    },
    {
        name: '金克丝',
        age: 14,
        say: '我是个疯子，有医生开的证明'
    },
    {
        name: '卢锡安',
        age: 15,
        say: '人终有一死 而有些人则需要一点小小的帮助'
    }
]
console.table(heroList)
```

![](https://user-gold-cdn.xitu.io/2020/3/13/170d33561ad66db9?w=828&h=110&f=png&s=6100)

那么打印`嵌套的对象数组`是什么样子呢：
```
let heroList = [
    {
        name: '小炮',
        age: 13,
        say: '我好想射点儿什么！',
        friend: {
            name: '锤石',
            age: 10
        }
    },
    {
        name: '金克丝',
        age: 14,
        say: '我是个疯子，有医生开的证明',
        friend: {
            name: '光辉',
            age: 11
        }
    },
    {
        name: '卢锡安',
        age: 15,
        say: '人终有一死 而有些人则需要一点小小的帮助',
        friend: {
            name: '琴女',
            age: 12
        }
    }
]
console.table(heroList)
```

![](https://user-gold-cdn.xitu.io/2020/3/13/170d3393ce860831?w=825&h=123&f=png&s=6927)
可以看到，friend字段折叠了，我使用的是Chrome浏览器，friend不能展开

### 计时 time timeLog timeEnd
通过计时器可以知道自己的代码运行多久的时间：
```
console.time('计时');
for(let i = 0; i < 10; i++) {
    // 其他代码
    console.timeLog('计时');
}
console.timeEnd('计时');
```

![](https://user-gold-cdn.xitu.io/2020/3/13/170d34245ed2e76f?w=224&h=226&f=png&s=7859)

不同电脑配置，不同运行环境，打印出来的时间会稍有差别，这很正常

### 其他控制台小技巧
#### 调试 debugger
有时候懒得打断点，可以试试`debugger`

```
function doSomething() {
    debugger
    console.log('英雄联盟不错')
}
// 调用
doSomething()
```
![](https://user-gold-cdn.xitu.io/2020/3/13/170d346a6889fafa?w=859&h=532&f=png&s=25536)

#### 快速选中元素 $0, $1, $2, $3, $4
怎么才能最快速地选中元素，其实也很简单，在浏览器的`Elements`面板中，鼠标最近点击的DOM元素就是$0，依次类推，还有$1, $2, $3, $4，以百度为例：

![](https://user-gold-cdn.xitu.io/2020/3/13/170d34cceff3ab80?w=1316&h=655&f=png&s=85337)

#### 另一种选中元素利器 `$`
相信大家都使用过`Jquery`，在`Jquery`中使用`$`来选择元素，浏览器也实现了`$`选择器。还是以百度为例：

![](https://user-gold-cdn.xitu.io/2020/3/13/170d353ea948f801?w=945&h=115&f=png&s=10240)


总结
最让我回味的功能是使用`%c`来写css样式，真是太惊艳了。好些网站都有自己的首页console，就像知乎那样。

### 参考
[css-tricks](https://css-tricks.com/a-guide-to-console-commands/)

[MDN console 文档](https://developer.mozilla.org/en-US/docs/Web/API/console)
