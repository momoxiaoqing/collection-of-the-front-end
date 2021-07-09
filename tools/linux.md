### linux操作
#### 查看文件大小 
```
df -h // 查看磁盘信息


du index-back.jpg -ah
du -h --max-depth=1 user  // 查看user文件夹下的子目录大小；-h：以K，M，G为单位，提高信息的可读性。
du -sh user  //查看user文件夹的大小
 ```
slkj@Idx365.com
#### 查找
```
sudo find / -name nginx*  //查找nginx
sudo find / -name "15900511*" // 查找含有‘15900511’内容的文件

grep test *file  //在当前目录中，查找后缀有 file 字样的文件中包含 test 字符串的文件，并打印出该字符串的行
grep -r update /etc/acpi // 查找指定目录/etc/acpi 及其子目录（如果存在子目录的话）下所有文件中包含字符串"update"的文件
grep -v test *test* // 反向查找，查找文件名中包含 test 的文件中不包含test 的行
```

#### 编辑
```
> test.txt // 清空文件
```

#### tomcat
##### 查看tomcat是否开启：`ps -ef|grep tomcat`
若结果是以下，则没有开启：
```
slkj     25289 25144  0 20:38 pts/0    00:00:00 grep tomcat
```

##### tomcat启动和关闭

在/usr/local/tomcat/bin目录下，开启：`./startup.sh`，关闭：`./shutdown.sh`

注意：
1、启动时报错：
```
Using CATALINA_PID:    /usr/local/tomcat-9.0.29/tomcat.pid
Existing PID file found during start.
Unable to read PID file. Start aborted.
```
删除/usr/local/tomcat-9.0.29/tomcat.pid后重新启动即可（centos 7）

2、启动后404，日志报错无权限，需要用sudo重启

3、接口504，重启nginx

##### 日志相关
用`nginx -t`查看日志地址，日志在log/catalina.out

* 从尾部查看：`tail -f catalina.out`
* 查看最近50行日志：`tail -n 50 -f catalina.out`
* 查看文件大小：`du -h catalina.out`
* 清除日志：`> catalina.out`


#### nginx 
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

##### 页面502
香港服务器：注释请求来源解析
