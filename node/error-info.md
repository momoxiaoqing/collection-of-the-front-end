### cannot find module 'express' {#cannot-find-module-express}

1、在项目目录内express --version 能显示版本号，但是执行node test.js时，却报错“ Cannot find module 'express' ............”

这是node安装目录和npm默认安装express的位置不同引起的。

解决方法：配置环境变量

NODE\_PATH：C:\Users\lenovo\AppData\Roaming\npm\node\_modules //实际express安装的目录+

2、在webstorm内debug时报错cannot find module 'express'

解决方法：在path增加C:\Users\lenovo\AppData\Roaming\npm\node\_modules

注意：需要重启电脑

