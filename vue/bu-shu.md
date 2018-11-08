### 路由配置基本路径

route文件中加入base:url

```
 base: '/shangyuyiyou-manage/',
 routes:[]
```

### 打包后static中文件404解决方法：

在config/index.js中修改默认加载路径

```
build:{
    assetsPublicPath: '/'
}
```

改为：

```
build:{
    assetsPublicPath: './'
}
```



