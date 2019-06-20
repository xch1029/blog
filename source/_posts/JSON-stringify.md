---
title: JSON.stringify
date: 2019-06-10 15:31:27
tags: javascript
---
![](https://user-gold-cdn.xitu.io/2019/6/20/16b74127890b575e?w=510&h=109&f=png&s=9883)
> - 作者: 小华坚决上王者
> - 建议阅读时间: 2 min
> - [掘金地址](https://juejin.im/post/5d0b45866fb9a07ed136db0f)

> JSON.stringify()是个经常使用的前端方法，这个函数可以传入三个参数，这里我安利下第三个参数，专门用来`美化输出`，先看下语法:

```
JSON.stringify(value[, replacer [, space]])
```

## 下面我列举了三个常用的例子，直接上代码

### 普通用法
``` javascript
let obj = {
  a: 'foo',
  b: 'bar',
}

console.log(JSON.stringify(obj))

// "{"a":"foo","b":"bar"}"
```

### space传入数字
``` javascript
let obj = {
  a: 'foo',
  b: 'bar',
}

console.log(JSON.stringify(obj, null, 2))

/*
{
  "a": "foo",
  "b": "bar"
}
*/
```

### space传入字符串
``` javascript
let obj = {
  a: 'foo',
  b: 'bar',
}

console.log(JSON.stringify(obj, null, '--'))

/*
{
--"a": "foo",
--"b": "bar"
}
*/
```

怎么样，是不是很爽，space传入数字应该可以满足大多数需求，我也推荐大家这么使用。