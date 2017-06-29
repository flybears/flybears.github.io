---
layout: "post"
title: "js数组去重的新方法"
date: "2017-06-29 20:04"
excerpt: "通过Set对js数组去重"
tags: [Set, 去重]
tech: true
comments: true
weather: rain
---


数组去重一直以来在项目中用的还是比较多的，以前基本上都是对数组通过一系列的循环操作实现去重，今天看了[稀土掘金](https://juejin.im)里面的一篇文章提到了ES6新出的`Set`对象，发现此对象能够很方便的实现数组去重。

# Set简述

> Set对象是值的集合，你可以按照插入的顺序迭代它的元素。 Set中的元素只会出现一次，即 Set 中的元素是唯一的。


# Set实现去重

``` javascript

    //例一
    const setObj = new Set();
    [1,1,1,1,2,2,2,3,3,3].forEach(x => setObj.add(x));

    for(let value of setObj){
        console.log(value);
    }
    console.log(setObj.size) //3
    //1,2,3

    //例二
    const setObj = new Set([1,1,1,1,2,2,2,3,3,3]);
    console.log(setObj.size); //3

    //例三
    const setObj = new Set([{a:1}, {a:1}, {}, {}]);
    console.log(setObj.size);//4

    //例四
    const x = {a: 1};
    const setObj = new Set([x, x]);
    console.log(setObj.size); //1

    //例四
    const setObj = new Set(["1", 1]);
    console.log(setObj.size); //2

    //例五
    const setObj = new Set([null, null]);
    console.log(setObj.size); //1

```


# 结论

- Set中两个值相等时可以实现去重，如果是对象数组，则引用相等时可实现去重。
- 虽然`null === null`值为false，但是Set还是可以实现去重。
- Set判断两个值是否相等时，不会做弱类型转换。


# 扩展（Set对象的属性和方法）

## 属性
- `Set.prototype.constructor`: 构造函数。
- `Set.prototype.size`: 返回实例的总数。

## 方法
- `add(value)`: Set实例中添加值，返回Set实例。
- `delete(value)`: 根据值删除元素，如果删除之前该元素存在，则返回true,否则这返回false。
- `clear()`: 移除Set对象内的所有元素，无返回值。
- `has(value)`: 该值是否在Set对象中存在，存在则为true,反之则为false。
- `forEach(callbackFn[, thisArg])`: 按照插入顺序，Set对象中的每个值都调用一次callbackFn，如果存在thisArg参数，则为Set对象中的值。
- `entries()`: 返回一个新的迭代器对象。

ps: delete对象只提供了通过值去删除，如果Set对象中的元素为对象，则不太好删除。
