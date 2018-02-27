### prop父子组件间数据交互

parent：

```
<template>
 <!-- <dynamics-list></dynamics-list>-->
  <div>
    <div v-for="(item,index) in dynamicsList" :key="index">
      <div v-if="item.publish_time">
       <!-- 以下表示把一个对象的所有属性作为 prop 进行传递-->
       <!-- <article-item v-bind="item" ></article-item>-->
       <!-- 等价于：-->
       <!-- <article-item :id="item.id" 
                          :title="item.title" 
                          :summary="item.summary" 
                          :publish_time="item.publish_time" ></article-item>-->
       
        <article-item :item="item" ></article-item>
      </div>
      <div v-else>
        <dlog-item :item="item" ></dlog-item>
      </div>
    </div>
  </div>
</template>
<script>
import articleItem from '../components/base/Article'
import dlogItem from '../components/base/Dlog'
export default {
  name: 'Home',
  data () {
    return {
      dynamicsList: [
        {
          id: 0,
          title: 'test1',
          summary: '这是一个文章。。。。。。',
          publish_time: '2018-02-27'
        },
        {
          id: 1,
          content: '这是一个dlog',
          create_time: '2018-02-26'
        }
      ]
    }
  },
  components: {
    // dynamicsList
    articleItem,
    dlogItem
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
```

Article.vue:

```js
<template>
  <div>
    {{article.title}}
  </div>
</template>

<script>
  export default {
    name: 'Article',
    props: ['item'],
    data () {
      return {
        article: this.item
      }
    }
  }
</script>

<style scoped>

</style>

```



