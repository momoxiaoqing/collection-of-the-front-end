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

#### Linux操作
##### 查看nginx是否开启：`ps -ef|grep nginx`
##### 启动
`nginx -c /etc/nginx/nginx.conf`

若报错:
```
nginx: [alert] could not open error log file: open() "/var/log/nginx/error.log" failed (13: Permission denied)
2020/12/04 11:18:52 [warn] 17220#0: the "user" directive makes sense only if the master process runs with super-user privileges, ignored in /etc/nginx/nginx.conf:5
2020/12/04 11:18:52 [emerg] 17220#0: mkdir() "/var/lib/nginx/tmp/client_body" failed (13: Permission denied)
```
加sudo