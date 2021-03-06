### axios

#### 1、引入：
```
$ npm install axios

$ bower install axios

<script src="[[https://unpkg.com/axios/dist/axios.min.js"></script>
```

#### 2、单个请求：
```
axios.get(url[, config])
axios.post(url[, data[, config]])
axios.put(url[, data[, config]])
axios.delete(url[, config])
```


#### 3、多个请求 await                     
```
axios.all(iterable)
axios.spread(callback)
```

例：
``` 
  axios.all([
       axiosWithToken.get(url1 + typeId),
       axiosWithToken.get(url2,{params:params})
            ]).then(axios.spread((res1, res2) => {
            }))
```

#### 4、统一设置属性，属性选项为option内属性

```
axios.defaults.baseURL = 'https://api.example.com';
axios.defaults.headers={
   token:getCookie('token')
 }

var instance = axios.create({
  baseURL: 'https://api.example.com',
  headers:{
     token:getCookie('token')
     }
});
instance.defaults.headers={ token:getCookie('token')}
```
#### [vue中axios的配置](../vue/axiospei-zhi.md)

#### 参考资料：[https://www.npmjs.com/package/axios](https://www.npmjs.com/package/axios)



