### 1、background-size单位为像素时放在background后才生效

### 2、img浏览器解析时会在图片底部加上3px,即img父元素莫名多了3px,解决方法：

`1、vertical-align: middle;`

`2、display：block;`

### 3、writing-mode: vertical-lr微信PC端内置浏览器无效，除规定width外，暂无解决方法

### ul的list-style

1、为outside时，微信浏览器中显示的标记靠右，inside时才靠左；

2、若li中存在float，最好用float：right；否则，标记会显示在右侧；

### 4、单行省略号需在display:block时，超出的长度才不会影响其他元素；

### 5、input outline

### 6、文字强制不换行：

```
white-space:nowrap;
```

### 适用所有css属性
```
initial  // 属性的初始值
inherit  // 父元素属性的值
unset //属性克继承，则父元素属性的值；否则，初始值
```

[属性的初始值查看](https://www.w3.org/TR/CSS2/propidx.html)
