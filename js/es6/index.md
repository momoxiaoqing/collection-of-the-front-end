### es6基础语法

#### 展开语法
1、语法：iterableObj可以是数组、字符串、对象（克隆和并对象用，外面必须是{}），拷贝赋值时是深拷贝
```
 //函数调用，剩余参数
myFunction(...iterableObj);

//数组、对象构造
[...iterableObj]; 
{...iterableObj};
```
2、兼容性：IE不支持
