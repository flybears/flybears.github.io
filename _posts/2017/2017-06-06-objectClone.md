---
layout: post
title: "Object拷贝"
date: "2017-06-07 16:15"
excerpt: "object深拷贝和浅拷贝"
tags: [Object, 拷贝, 深拷贝, 浅拷贝]
tech: true
comments: true
weather: sun
---


在项目中我们经常会遇见对源对象不进行操作，而需要拷贝对象，`Object` 拷贝分为浅拷贝和深拷贝。

## 浅拷贝的实现

### 1、 Object.assign()

``` javascript

    var o = {key: 1};
    var cloneObject = Object.assign({}, o);
    cloneObject.key = 2;
    console.log(o.key); // 1

    var nest = {key: {nest: 1}};
    var nestObject = Object.assign({}, nest);
    nestObject.key.nest = 2;
    console.log(nest.key.nest) // 2

```

### 2、手动实现

``` javascript

    function simpleCopy(obj){
        var cloneObj = {};
        for(var key in obj){
            if(obj.hasOwnProperty(key)){
                cloneObj[key] = obj[key];
            }
        }
        return cloneObj;
    }

```



## 深拷贝
### 1、JSON.parse()和JSON.stringify()

``` javascript

    var o = {
        a: {
            aa: 1,
            ab: 2
        }
    };

    var cloneObj = JSON.parse(JSON.stringify(o));
    cloneObj.a.aa = 2;
    console.log(o.a.aa); // 1

```

### 2、手动实现

``` javascript

    function deepCopy(obj){
        var copy;
        if(!obj || "object" != typeof obj){
            return obj;
        }
        copy = Object.prototype.toString.call(obj).slice(8, -1) == "Array" ? [] : {};
        for(var key in obj){
            if(obj.hasOwnProperty(key)){
                copy[key] = deepCopy(obj[key]);
            }
        }
        return copy;
    }

```

** 注: 数组如果是对象数组，用slice拷贝，则里面的对象不是深拷贝。 **
