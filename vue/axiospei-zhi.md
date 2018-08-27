### axios.config.js

```js
import router from 'vue-router'
import axios from 'axios'
import {Message} from 'element-ui'

const networkErr = '网络错误，请重试'

if (process.env.NODE_ENV === 'development') {
  axios.defaults.baseURL = '/webapi'
} else if (process.env.NODE_ENV === 'debug') {
  axios.defaults.baseURL = ''
} else if (process.env.NODE_ENV === 'production') {
  axios.defaults.baseURL = 'http://api.123dailu.com/'
}

// 请求超时时间
axios.defaults.timeout = 10000

// post请求头
axios.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded;charset=UTF-8'
axios.defaults.headers.common['access-token'] = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE1MzU3ODY2MDgsImlhdCI6MTUzNDkyMjYwOCwidG9rZW4iOiJ7XCJjbGllbnRcIjpcIndlYlwiLFwicm9sZUNvZGVcIjpcIjAwMTExMTExMTExMTExMTFcIixcInVzZXJJZFwiOjEsXCJ1c2VyTmFtZVwiOlwiYWRtaW5cIn0ifQ.LEkDtsgJD5rx70LvtGywKe8pVIc5LIGIekuZnk1d83s'

// 请求拦截器
axios.interceptors.request.use(
  config => {
    // 每次发送请求之前判断是否存在token，如果存在，则统一在http请求的header都加上token，不用每次请求都手动添加了
    // 即使本地存在token，也有可能token是过期的，所以在响应拦截器中要对返回状态进行判断
    let token = localStorage.getItem('token')
    token && (config.headers.common['access-token'] = token)
    console.log(config)
    return config
  },
  error => {
    return Promise.error(error)
  })

// 响应拦截器
axios.interceptors.response.use(
  response => {
    if (response.status === 200) {
      if (response.data.success === 1) {
        return Promise.resolve(response.data.data)
      } else {
        // let code = response.data.error.code
        let message = response.data.error.message
        /* switch (code) {
         case '1100': message
        } */
        Message.error(message || networkErr)
      }
      // return response.data.success === 1 ? Promise.resolve(response.data.data) : Promise.reject(response.data.error.message)
    } else {
      // return Promise.reject(response)
      Message.error(response.data.error.message || networkErr)
    }
  },
  // 服务器状态码不是200的情况
  error => {
    debugger
    if (error.response.status) {
      switch (error.response.status) {
        // 401: 未登录
        // 未登录则跳转登录页面，并携带当前页面的路径
        // 在登录成功后返回当前页面，这一步需要在登录页操作。
        case 401:
          router.replace({
            path: '/login',
            query: {redirect: router.currentRoute.fullPath}
          })
          break
        // 403 token过期
        // 登录过期对用户进行提示
        // 清除本地token和清空vuex中token对象
        // 跳转登录页面
        case 403:
          Message.error('登录过期，请重新登录')
          // 清除token
          localStorage.removeItem('token')
          this.$store.commit('loginSuccess', null)
          // 跳转登录页面，并将要浏览的页面fullPath传过去，登录成功后跳转需要访问的页面
          setTimeout(() => {
            router.replace({
              path: '/login',
              query: {
                redirect: router.currentRoute.fullPath
              }
            })
          }, 1000)
          break
        // 404请求不存在
        case 404:
          Message.error('网络请求不存在')
          break
        // 其他错误，直接抛出错误提示
        default:
          Message.error('error.response.data.message')
      }
      // return Promise.reject(error.response)
      Message.error(networkErr)
    }
  }
)

export default axios
```

### main.js

```js
import axios from './api/axios.config'

Vue.prototype.axios = axios
```

### 应用 

```
this.axios.post()
```



