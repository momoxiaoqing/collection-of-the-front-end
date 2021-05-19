### promise相关
#### 打印相关
```javascript
var p = new Promise((resolve, reject) => {
    reject(Error('The Fails!')) //return reject(Error('The Fails!')) 同效
})
p.catch(error => console.log(error))

var p = new Promise((resolve, reject) => {
    reject(Error('The Fails!')) //return reject(Error('The Fails!')) 同效
}).catch(error => console.log(error))

// 打印报错
// Error: The Fails!
//      at <anonymous>:3:12
//      at new Promise (<anonymous>)
//      at <anonymous>:1:9
```

```javascript
var p = new Promise((resolve, reject) => {
  return Promise.reject(Error('The Fails!'))
})
p.catch(error => console.log(error.message))

// 
```