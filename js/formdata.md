### 1、作用：

发送表单数据，通过FormData传输的数据格式和表单（编码类型为multipart/form-data）通过submit\(\) 方法传输的数据格式相同



### 2、运用场景：

   在表单提交时，添加用户没有输入的内容

   上传文件



### 3、创建FormData对象：

```js
var formData = new FormData();
//通过html创建
var formData = new FormData(someFormElement);
//添加内容
formData.append("username", "Groucho");
```



### 4、常用方法：

```js
FormData.append()
FormData.delete()
FormData.get()
FormData.has()
FormData.keys()
FormData.set()
FormData.values()
```

5、例子

