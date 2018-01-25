起步：[https://github.com/nswbmw/N-blog](https://github.com/nswbmw/N-blog)

### cannot find module 'express'

1、在项目目录内express --version 能显示版本号，但是执行node test.js时，却报错“ Cannot find module 'express' ............”

这是node安装目录和npm默认安装express的位置不同引起的。

解决方法：配置环境变量

NODE\_PATH：C:\Users\lenovo\AppData\Roaming\npm\node\_modules    //实际express安装的目录

2、在webstorm内debug时报错cannot find module 'express'

解决方法：在path增加C:\Users\lenovo\AppData\Roaming\npm\node\_modules

注意：需要重启电脑

### supervisor

监听当前目录下 node 和 js 后缀的文件，当这些文件发生改动时，supervisor 会自动重启程序。

安装：npm install -g supervisor

运行：supervisor --harmony index

