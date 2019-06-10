---
title: JSON.stringify
date: 2019-06-10 15:31:27
tags: javascript
---

今天看到一篇介绍JSON.stringify，原来这个函数可以传入三个参数，这里我安利下第三个参数，专门用来美化输出的，先看下语法:

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