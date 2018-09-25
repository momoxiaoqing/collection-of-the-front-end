### 一、一般规范

1、文件名

小写，“-连接”，如：

```
my-script.js
my-camel-case-name.css
i-love-underscores.html
thousand-and-one-scripts.js
my-file.min.css
```

2、协议

不要指定引入资源所带的具体协议。

当引入图片或其他媒体文件，还有样式和脚本时，URLs 所指向的具体路径，不要指定协议部分（`http:`,`https:`），除非这两者协议都不可用。

不指定协议使得 URL 从绝对的获取路径转变为相对的，在请求资源协议无法确定时非常好用，而且还能为文件大小节省几个字节。

```
<script src="//cdn.com/foundation.min.js"></script>

.example {
  background: url(//static.example.com/images/bg.jpg);
}
```

### 二、html

1、脚本加载

所有浏览器中，推荐：

```
<html>
  <head>
    <link rel="stylesheet" href="main.css">
  </head>
  <body>
    <!-- body goes here -->

    <script src="main.js" async></script>
  </body>
</html>
```

只在现代浏览器中，推荐：

```
<html>
  <head>
    <link rel="stylesheet" href="main.css">
    <script src="main.js" async></script>
  </head>
  <body>
    <!-- body goes here -->
  </body>
</html>
```

2、微格式

在 SEO 和可用性上的运用

3、IIFE（立即执行的函数表达式）

推荐：

```
(function(){}());
```

如果你想引用全局变量或者是外层 IIFE 的变量，可以通过下列方式传参：

```
(function($, w, d){
  'use strict';

  $(function() {
    w.alert(d.querySelectorAll('div').length);
  });
}(jQuery, window, document));
```

### 三、js

1、申明多个变量，推荐：

```
var a = 10,
    b = 10,
    c = 100;
```

2、异常

在复杂的环境中，你可以考虑抛出对象而不仅仅是字符串（默认的抛出值）。

```
if(name === undefined) {
  throw {
    name: 'System Error',
    message: 'A name should always be specified!'
  }
}
```

### 四、css

1、命名

```
#video-id {}
.ads-sample {}
```

2、不使用 直接子选择器可能会导致疼痛的设计问题并且有时候可能会很耗性能。如果你不写很通用的，需要匹配到DOM末端的选择器， 你应该总是考虑直接子选择器。

不推荐：

```
.content .title {
  font-size: 2rem;
}
```

推荐：

```
.content > .title {
  font-size: 2rem;
}
```

3、声明顺序

```js
//结构性属性：
display
position, left, top, right etc.
overflow, float, clear etc.
margin, padding
//表现性属性：
background, border etc.
font, text
```

4、多个选择器分离

```
h1,
h2,
h3 {
  font-weight: normal;
  line-height: 1.2;
}
```

5、引号

属性选择器或属性值用双引号（””），而不是单引号（”）括起来。

URI值（url\(\)）不要使用引号。

```
@import url(//cdn.com/foundation.css);

html {
  font-family: "open sans", arial, sans-serif;
}

body:after {
  content: "pause";
}
```



