### Vue CLI 2版本

#### 1、路由配置基本路径

route文件中加入base:url

```
 base: '/shangyuyiyou-manage/',
 routes:[]
```

#### 2、打包后static中文件404解决方法：

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

#### 3、element-icons.woff文件404
在build/utils文件中添加  publicPath:'../../'
```
  if (options.extract) {
      return ExtractTextPlugin.extract({
        use: loaders,
        fallback: 'vue-style-loader',
        publicPath:'../../'   // 添加
      })
    } else {
      return ['vue-style-loader'].concat(loaders)
    }
```


vue/cli 3没有这个问题，已无config中已无build，无需修改

### Vue CLI 3版本

因为在route中默认：

```
base: process.env.BASE_URL //vue.config.js中配置的publicPath
```

所以在vue.config.js中定义publicPath就可以，建议：

```
 publicPath: process.env.NODE_ENV === 'production'
        ? './'
        : '/qing-he-yang-rong-manager',
```



