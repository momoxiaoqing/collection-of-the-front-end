### eslintrc规范中去掉缩进

在.eslintrc.js的rules中加入：

```
'indent': 'off'
```

### vue组件加载图片：

assets和static文件夹中图片均可放：

```js
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



