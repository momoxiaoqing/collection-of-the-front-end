### eslintrc规范中

1、在.eslintrc.js的rules中加入：

```
'indent': 'off'//缩进

// 注释
'beforeBlockComment': true,
'beforeLineComment': true
```

2、记录
* 忽略下行规范：/* eslint-disable no-unused-vars */

### vue组件加载图片：

assets和static文件夹中图片均可放：

```
<template>
    <div>
        <h1>{{ss}}</h1>
        <img class="preview-img" v-for="(item, index) in list" :src="item.src" :key="index" height="100"
             @click="$preview.open(index, list)">
        <img src="../assets/1.jpg" alt="">
    </div>
</template>

<script>
    import img from './../assets/1.jpg'
    export default {
        name: 'Page1',
        data () {
            return {
                ss: 'photoswipe test',
                list: [{
                    src: img,
                    w: 600,
                    h: 400
                }, {
                    src: 'static/1.jpg',
                    w: 1200,
                    h: 900
                }]
            }
        }
    }
</script>
```

区别：assets在build时会被打包，而static不会

### 

### 取消mySwiper未被使用的报错

添加注释：

```
/* eslint-disable no-unused-vars */
let test = 1
```

### v-show

v-show不支持&lt;template&gt;

### 

### 修改插件

建议先fork插件，再将其替换成修改好的文件，运行npm install [https://github.com/momoxiaoqing/vue-preview.git](https://github.com/momoxiaoqing/vue-preview.git) -s，或直接修改json文件，再npm install

```
"vue-preview": "https://github.com/momoxiaoqing/vue-preview.git"


```

### 添加动态属性 $set

```
 export default {
        name: 'test',
        data () {
            return {
                user: {}
            }
        },
        methods: {
            getUser () {
                // 添加动态属性
                this.user.userName='111' // Vue 无法探测普通的新增属性
                this.user = {
                    userName: '123'
                } // 响应式属性
                this.$set(this.user,'userName','123') // 响应式属性
            }
        }
    }
```



