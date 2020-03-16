---
title: 2020年，你必须知道的JS数组技巧
date: 2020-02-19 23:24:16
tags: Javascript
---
在Javascript中，数组是一个重要且常见的知识点，我们经常将数据存储在数组中。作为一名Javascript工程师，数组必须要运用自如。这篇文章，向大家展示了在日常开发中，数组有哪些奇淫技巧值得关注和学习，让我们开始吧！

### 1.去重
这也是一道常见的面试题，怎么对JS的数组去重。在ES6的时代，有个非常快速且简单的方法，使用`new Set()`以及`Array.from()`或者`展开运算符(...)`
``` javascript
var fruits = [“banana”, “apple”, “orange”, “watermelon”, “apple”, “orange”, “grape”, “apple”];


// 方法一
var uniqueFruits = Array.from(new Set(fruits));
console.log(uniqueFruits); // returns [“banana”, “apple”, “orange”, “watermelon”, “grape”]
// 方法二
var uniqueFruits2 = […new Set(fruits)];
console.log(uniqueFruits2); // returns [“banana”, “apple”, “orange”, “watermelon”, “grape”]
```

### 2.替换
日常开发中经常需要替换或者删除一些指定的数据，遇到这种场景时一定要联想到`Array.protoType.splice`这个方法。传参时稍微复杂点，第一个参数是开始的索引，第二个参数是需要删除的数量，剩下的就是需要添加的值（可以是一个或者多个）。
```javascript
var fruits = [“banana”, “apple”, “orange”, “watermelon”, “apple”, “orange”, “grape”, “apple”];
fruits.splice(0, 2, “potato”, “tomato”);
console.log(fruits); // returns [“potato”, “tomato”, “orange”, “watermelon”, “apple”, “orange”, “grape”, “apple”]
```

### 3.遍历数组
平时我们使用最多的就是数组的`.map`方法，其实还有一个方法也能达到一样的目的，用法比较冷门，所以我们总是忽视，那就是`Array.from`
```javascript
var friends = [
    { name: ‘John’, age: 22 },
    { name: ‘Peter’, age: 23 },
    { name: ‘Mark’, age: 24 },
    { name: ‘Maria’, age: 22 },
    { name: ‘Monica’, age: 21 },
    { name: ‘Martha’, age: 19 },
]

var friendsNames = Array.from(friends, ({name}) => name);
console.log(friendsNames); // returns [“John”, “Peter”, “Mark”, “Maria”, “Monica”, “Martha”]
```

### 4.清空数组
有时我们需要清空一个数组，比如用户点击了清空购物车。可以一条一条地删除，但是很少有这么可爱的程序员，哈哈。其实一行代码就能搞定，那就是直接将之`length`设置成0
```
var fruits = [“banana”, “apple”, “orange”, “watermelon”, “apple”, “orange”, “grape”, “apple”];

fruits.length = 0;
console.log(fruits); // returns []
```

### 5.数组转换成对象
有时候需要将数组转换成对象的形式，使用`.map()`一类的迭代方法能达到目的，这里还有个更快的方法，前提是你正好希望对象的key就是数组的索引
``` javascript
var fruits = [“banana”, “apple”, “orange”, “watermelon”];
var fruitsObj = { …fruits };
console.log(fruitsObj); // returns {0: “banana”, 1: “apple”, 2: “orange”, 3: “watermelon”, 4: “apple”, 5: “orange”, 6: “grape”, 7: “apple”}
```

### 6.填充数组
创建数组的时候，你有没有遇到过需要填充上默认值的场景，你肯定首先想到的就是循环这个数组。ES6提供了更便捷的`.fill`方法
```  javascript
var newArray = new Array(10).fill(“1”);
console.log(newArray); // returns [“1”, “1”, “1”, “1”, “1”, “1”, “1”, “1”, “1”, “1”, “1”]
```

### 7.合并数组
你知道如何合并数组吗，答案就是`.concat()`。哈哈，但是今天的主角是ES6的展开运算符(...)
``` javascript
var fruits = [“apple”, “banana”, “orange”];
var meat = [“poultry”, “beef”, “fish”];
var vegetables = [“potato”, “tomato”, “cucumber”];
var food = […fruits, …meat, …vegetables];
console.log(food); // [“apple”, “banana”, “orange”, “poultry”, “beef”, “fish”, “potato”, “tomato”, “cucumber”]
```

### 8.两个数组的交集
找出两个数组的交集算是一道经典的JS面试题了，这题能很好地考察候选人的逻辑是否清晰，对数组的掌握是否熟练。这题的答案有很多，下面展示的是ES6的简洁写法
```
var numOne = [0, 2, 4, 6, 8, 8];
var numTwo = [1, 2, 3, 4, 5, 6];
var duplicatedValues = […new Set(numOne)].filter(item => numTwo.includes(item));
console.log(duplicatedValues); // returns [2, 4, 6]
```

### 9.去除假值
首先，我们熟悉下假值(falsy values)是什么？在JS中，假值有：`false`、`0`、`''`、`null`、`NaN`、`undefined`。现在我们找到这些假值并将它们移除，这里使用的是`.filter`方法
``` javascript
var mixedArr = [0, “blue”, “”, NaN, 9, true, undefined, “white”, false];
var trueArr = mixedArr.filter(Boolean);
console.log(trueArr); // returns [“blue”, 9, true, “white”]
```

### 10.随机值
从数组中获取随机的一个值，也是一道经典的面试题哦。其实考察的核心知识是随机生成一个值x：x >= 0 并且 x < 数组的length
``` javascript
var colors = [“blue”, “white”, “green”, “navy”, “pink”, “purple”, “orange”, “yellow”, “black”, “brown”];
var randomColor = colors[(Math.floor(Math.random() * (colors.length)))]
```

### 11.倒序
怎么对数组进行倒序？只需要一行代码
``` javascript
var colors = [“blue”, “white”, “green”, “navy”, “pink”, “purple”, “orange”, “yellow”, “black”, “brown”];
var reversedColors = colors.reverse();
// 或者 colors.slice().reverse();
// 两者有啥区别？
console.log(reversedColors); // returns [“brown”, “black”, “yellow”, “orange”, “purple”, “pink”, “navy”, “green”, “white”, “blue”]
```

### 12.lastIndexOf()
很多时候我们查找元素是否存在于某个数组中，经常使用`indexOf`方法，常常忽略`lastIndexOf`方法，后者会被使用的一个场景就是，某个数组中有重复的数据。
``` javascript
var nums = [1, 5, 2, 6, 3, 5, 2, 3, 6, 5, 2, 7];
var lastIndex = nums.lastIndexOf(5);
console.log(lastIndex); // returns 9
```

### 13.求和
对数组中的所有元素进行求和，哈哈，又是一道如数家珍的面试题。答案也是很多，条条大道通罗马，这里使用的是`reduce`，`reduce`方法是很值得学习的知识点，用处很多。
```
var nums = [1, 5, 2, 6];
var sum = nums.reduce((x, y) => x + y);
console.log(sum); // returns 14
```

### 总结
这篇文章，向小伙伴们展示了在JS中怎么去操作数组的种种技巧，其实在日常开发中，很可能还会遇到更加复杂的业务，希望你们能一一解剖成小问题，找到入手的地方。加油小伙伴们！

> [原文链接](https://dev.to/duomly/13-useful-javascript-array-tips-and-tricks-you-should-know-2jfo)