---
layout: post
title: "div垂直水平居中的几种方式"
date: "2017-05-26 11:15"
excerpt: "div垂直水平居中的几种方式"
tags: [html, div, 盒子, 垂直居中]
tech: true
comments: true
weather: sun
---

## 现状
> div的水平居中还是很好实现的，但是垂直居中这块比较的麻烦。css中有个`vertical-align`属性，这个属性比较的麻烦，有些同学用的时候经常会觉得无效。所以这篇博客会着重介绍下div垂直方面的知识。

## 实现方式

### 1、table-cell方式
html:
``` html
    <div class="container">
        <div class="box"></div>
    </div>
```

css:
``` css
    .container{
        width: 500px;
        height: 500px;
        display: table-cell;
        vertical-align: middle;
        background: black;
    }

    .box{
        width: 100px;
        height: 100px;
        background: red;
        margin: 0 auto;
    }
```

### 2、line-height
html同上

css:
``` css
    .container{
        width: 500px;
        height: 500px;
        line-height: 500px;
        text-align: center;
        background: black;
    }

    .box{
        width: 100px;
        height: 100px;
        vertical-align: middle;
        background: red;
        display: inline-block;
    }
```

### 3、position
html同上

css:
``` css
    .container{
    	width: 500px;
    	height: 500px;
    	background: black;
    	position: relative;
    }

    .box{
    	width: 100px;
    	height: 100px;
    	background: red;
    	position: absolute;
    	top: 50%;
    	left: 50%;
    	/*margin-left: -50px;
    	margin-top: -50px;*/
    	transform: translate(-50%, -50%);
    }
```

### 4、新旧版弹性盒子模型
html同上

css:
``` css
    .container{
        width: 500px;
        height: 500px;
        background: black;
        /*display: flex;
        justify-content: center;
        align-items: center;*/

        display:box;
        box-pack:center;
        box-align:center;

        /* Firefox */
        display:-moz-box;
        -moz-box-pack:center;
        -moz-box-align:center;

        /* Safari、Opera 以及 Chrome */
        display:-webkit-box;
        -webkit-box-pack:center;
        -webkit-box-align:center;


    }

    .box{
        width: 100px;
        height: 100px;
        background: red;
    }
```
