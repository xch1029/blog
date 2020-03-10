---
title: JS中的高阶函数
date: 2020-03-08 21:24:55
tags: Javascript
---

“高阶函数”是个我们经常遇到的术语，英文名叫“higher-order function”，对于新手而言，还挺神秘。今天，我们就来探讨下高阶函数。

### 定义
**接收函数作为参数或者返回函数的函数**

大白话就是：
1. 首先是个函数
2. 参数或者返回值是函数

### 举例子
我们这里举两个例子来覆盖下上文的定义，其中，例一为`接收函数`作为参数的高阶函数，例二为`返回函数`的高阶函数。

#### 例一：函数作为参数
我们定义了一个叫`evaluatesToFive`的函数，接收两个参数：第一个参数是一个数字，第二个参数是一个函数。在函数`evaluatesToFive`中，将参数一(数字)传入参数二(函数)

```
function evaluatesToFive(num, fn) {
  return fn(num) === 5;
}
```
使用的场景：
```
function divideByTwo(num) {
  return num / 2;
}

evaluatesToFive(10, divideByTwo);
// true

evaluatesToFive(20, divideByTwo);
// false
```
哈哈，虽然函数本身用处不大，但是对描述高阶函数来说，很简单易懂。

#### 例二：返回函数
本例中，我们创建函数`multiplyBy`，接收一个数字作为参数，并返回一个新的函数

```
function multiplyBy(num1) {
  return function(num2) {
    return num1 * num2;
  };
}
```

使用场景：
```
const multiplyByThree = multiplyBy(3);
const multiplyByFive = multiplyBy(5);

multipyByThree(10); // 30

multiplyByFive(10); // 50
```

是不是有点感觉了，通过生成新的函数以达到更具体的目的。

### 更复杂的应用实例
本例中，我们创建一个函数去检测新用户的注册信息是否能通过检验规则：
- 大于18岁
- 密码长度大于8
- 同意用户协议

新用户的注册信息大概是这样：
```
const newUser = {
  age: 24,
  password: 'some long password',
  agreeToTerms: true,
};
```

接下来，我们来创建三个验证函数，通过返回`true`，否则返回`false`
```
function oldEnough(user) {
  return user.age >= 18;
}

function passwordLongEnough(user) {
  return user.password.length >= 8;
}

function agreeToTerms(user) {
  return user.agreeToTerms === true;
}
```
接下来，该主角登场了，我们需要创建一个高阶函数来一次性完成所有的验证。参数一是新用户注册信息，剩下的参数是我们上文创建的三个验证函数。在函数体中依次执行验证：
```
function validate(obj, ...tests) {
  for (let i = 0; i < tests.length; i++) {
    if (tests[i](obj) === false) {
      return false;
    }
  }
  return true;
}
```
使用：
```
const newUser1 = {
  age: 40,
  password: 'tncy4ty49r2mrx',
  agreeToTerms: true,
};

validate(newUser1, oldEnough, passwordLongEnough, agreeToTerms);
// true

const newUser2 = {
  age: 40,
  password: 'short',
  agreeToTerms: true,
};

validate(newUser2, oldEnough, passwordLongEnough, agreeToTerms);
// false
```
到目前为止，已经很棒了，继续看下去，看我们怎么改进

### 继续进化

上文中，我们使用`validate`函数的时候需要传入多个验证函数(oldEnough, passwordLongEnough, agreeToTerms)，这违反了`最少知识原则`(有兴趣的同学们可以去了解下[最少知识原则](https://baike.baidu.com/item/%E8%BF%AA%E7%B1%B3%E7%89%B9%E6%B3%95%E5%88%99/2107000?fromtitle=%E6%9C%80%E5%B0%91%E7%9F%A5%E8%AF%86%E5%8E%9F%E5%88%99&fromid=11187352&fr=aladdin))，看我们怎么将之继续改进：
```
function createValidator(...tests) {
  return function(obj) {
    for (let i = 0; i < tests.length; i++) {
      if (tests[i](obj) === false) {
        return false;
      }
    }
    return true;
  };
}
```
这个`createValidator`函数牛逼了，它接收任意数量的函数作为参数，返回值也是个函数。所以这个`createValidator`也是个高阶函数。

使用：
```
const userValidator = createValidator(
  oldEnough,
  passwordLongEnough,
  agreeToTerms
);

userValidator(newUser1); // true
userValidator(newUser2); // false

```

看出什么门道了没？通过函数`createValidator`生成更具体的验证函数`userValidator`，再使用`userValidator`去验证新用户的注册信息。多么精彩的高阶函数！意犹未尽的同学们可以再学习下另一个术语`柯里化`！

### 结语
本小文，我们一起探讨了JS中的高阶函数，千万不要以为高阶函数只是一道面试题。前端框架中很火的`高阶组件`也是引用自高阶函数。高阶函数在我们日常开发中经常会使用到，用好了，可以将很多复杂的业务逻辑进行解耦，对于代码的可读性和可维护性很有意义！文中也用到了闭包的知识，聪明的你发现了吗？不要让自己的知识永远躺在面试题中哦！
