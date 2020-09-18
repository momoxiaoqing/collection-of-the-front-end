### iframe
```
<iframe id="id" name="iframe"  src="test.html"></iframe>
```

#### 获取iframe内容
```
document.getElementsByTagName('iframe')[0].contentDocument.body.innerHTML
frames['iframe1'].document.body.innerHTML
document.getElementById('id').contentWindow.document.body.innerHTML
```

#### 判断是否加载完成
iframe加载需要时间，会导致获取iframe内容/手动添加link失败
加载完后再执行相关操作：

```
 if (iframe.attachEvent){     //IE
     iframe.attachEvent("onload", function(){
         // ...
     });
 } else {
     // ....
 }
```

#### 动态添加
html():
```
$('#test').html('<iframe name="iframe" id="id"  src="test.html" ></iframe>');
```
手动创建DOM：
```
var iframe = document.createElement("iframe");
iframe.src = url;
iframe.id=1;

// 插入
document.getElementById('test').appendChild(iframe);
```

#### 遍历
```
 $('iframe').each(function(){
     function injectCSS(){
         $iframe.contents().find('head').append(
             $('<link/>', { rel: 'stylesheet', href: '../css/introduce.css', type: 'text/css' })
         );
     }

     var $iframe = $(this);
     $iframe.on('load', injectCSS);
     injectCSS();
 });
```