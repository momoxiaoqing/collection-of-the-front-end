### 1、作用：

发送表单数据，通过FormData传输的数据格式和表单（编码类型为multipart/form-data）通过submit\(\) 方法传输的数据格式相同

### 

### 2、运用场景：

在表单提交时，添加用户没有输入的内容

上传文件

### 

### 3、创建FormData对象：

```js
var formData = new FormData();
//通过html创建
var formData = new FormData(someFormElement);
//添加内容
formData.append("username", "Groucho");
```

### 

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

### 

### 5、例子

```
<div class="picture_block">
    封面图片：
    <form @submit.prevent="upload" id="img-form" enctype="multipart/form-data">
        <input id="files" type="file" name="files" @change="preview">
        <!--<input id="files" type="file" name="files" @change="upload" >-->
        <div class="preview">预览：
            <span>
                <img :src="editor.preview||editor.data.coverUrl" alt="">
            </span>
        </div>
        <!--<input type="submit" value="上传" id="upload" style="">-->
    </form>
</div>
```

```js
var target=document.getElementById('img-form');
var data = new FormData(target);
axios.post('/attach/upload',data).then(function (res1) {
    if(res1.data.success){
        params.coverUrl=res1.data.data.url;
        if(app.checkIndex>=app.caseIndex){
            addCaseArticle(params)
        }else{
            addArticle(params)
        }
    }else{
        layer.msg(res1.data.message)
    }
});
```

### 

### 6、参考

[https://developer.mozilla.org/zh-CN/docs/Web/API/FormData/Using\_FormData\_Objects](https://developer.mozilla.org/zh-CN/docs/Web/API/FormData/Using_FormData_Objects)

[https://developer.mozilla.org/en-US/docs/Web/API/FormData](https://developer.mozilla.org/en-US/docs/Web/API/FormData)

