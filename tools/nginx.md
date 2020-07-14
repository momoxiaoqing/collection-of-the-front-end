### nginx 
#### 操作
* 测试配置：```nginx -t```
* cmd检查nginx是否启动成功：```tasklist /fi "imagename eq nginx.exe"```
* cmd关闭：```taskkill /f /t /im nginx.exe```


#### 本地ip不能访问
nginx localhost可以访问，本地ip不能访问：设置-网络和Intenet-代理，关闭代理


#### config
##### 1.文件上传限制
在http,serve中设置client_max_body_size都可以
```
client_max_body_size 20m;
```
