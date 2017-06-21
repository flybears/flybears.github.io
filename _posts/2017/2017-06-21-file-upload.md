---
layout: "post"
title: "文件上传"
date: "2017-06-21 09:41"
excerpt: "文件上传的几种实现方式"
tags: [文件, 上传]
tech: true
comments: true
weather: sun
---


文件上传是项目中用常用的操作之一，目前很多开源的前端框架都会带有文件上传，实现方式也有多种。

1. form表单提交方式
form表单上传是我们最常用的一种，用法也非常的简单。

``` html
<form action="https://jsonplaceholder.typicode.com/posts/" method="post" enctype="multipart/form-data">
    <input type="file" name="upload">
    <input type="submit" value="upload">
</form>
```

2. ajax + formData方式

``` html
<!-- 进度条 -->
<progress id="uploadProgress" min="0" max="100" value="0">0</progress>
<input type="file" id="file"/>
<input type="button" id="upload" value="upload" />
```

``` javascript
var upload = document.getElementById("upload");
upload.onclick = function(){
    var formData = new FormData();
    var request = new XMLHttpRequest();
    formData.append("files", document.getElementById("file").files[0]);
    request.open("post", "https://jsonplaceholder.typicode.com/posts/", true);
    request.onload = function(){
        if(request.status == 200){
            console.log("上传成功...");
        }else{
            console.log("上传失败...");
        }
    }
    request.upload.progress = function(event){
        if(event.lengthComputable){
            var complete = (event.loaded / event.total * 100 | 0);
            var progress = document.getElementById("uploadProgress");
            progress.value = progress.innerHTML = complete;
        }
    }
    request.send(formData);
}
```


3. flash上传
比较古老的一种上传实现方式，目前最新的chrome把flash默认关闭，所以建议用以上两种方式。
