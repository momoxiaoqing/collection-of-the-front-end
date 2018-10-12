### 一、命名：

1、必须以大写字母开头



### 二、props

1、传递字符串：

```js
<Welcome name="Tony"></Welcome>
```

2、传递变量

```js
const user = {
    name: 'Tony'
};

const el = (
   <Welcome name={user.name}></Welcome>
);
```



