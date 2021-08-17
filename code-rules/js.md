### js规范
变量命名
* export一个结构体/类/单例/函数库/对象时用大驼峰
* export函数时用小驼峰
* 类命令：大驼峰
* 常量命名：大写字符, 并用下划线分隔

变量创建
* 使用计算属性名创建一个带有动态属性名的对象
* 用对象的方法简写函数属性
* 用扩展运算符做数组浅拷贝 `b=[...a]`
* 用Array.from将一个类数组对象转成一个数组
* 多个返回值用对象的解构，而不是数组解构
* 当需要动态生成字符串时，使用模板字符串而不是字符串拼接 `How are you, ${name}?`

函数
* 使用函数表达式而不是函数声明 `const func = function () {}`
* 不要在非函数块（if、while等）内进行函数声明，而是把这个函数分配给一个变量
* 使用拓展运算符调用多参数的函数
* 调用或者声明一个包含多个参数的函数时，每个参数独占一行，每行逗号结尾
* 箭头函数的函数体由单个表达式语句组成时，省略大括号和 return
* 一个函数的长度控制在100行以内
* 一个函数的参数控制在6个以内

class
* 使用class语法。避免直接操作prototype
* 类的成员函数返回this来实现链式调用
* 空的类构造函数无需声明，直接省略
* 类的继承方案，实现时需要修正constructor

模块
* 使用（import/export）导入导出模块，避免使用require
* 避免使用import通配符，即import *这种方式
* 一个路径只import一次
* 一个import导入多个模块时，每个模块独占一行

控制语句、作用域与表达式
* 避免使用迭代器。需要时使用JavaScript高级特性代替：for-in、for-of
* 在case和default分句里用大括号创建一块包含词法声明的块
* 不要在循环体中包含函数表达式，事先将函数提取到循环体外
* 对有序集合进行顺序无关的遍历时，使用逆序遍历
* 类型检测优先使用typeof，对象类型检测使用instanceof，null或undefined的检测使用== null
* 避免使用continue语句
* 减少 delete 的使用
* for in 遍历对象时, 使用 hasOwnProperty 过滤掉原型中的属性

类型转换
* 转换成number时，使用+
* string转换成number，要转换的字符串结尾包含非数字并期望忽略时，使用parseInt
* 使用parseInt时，必须指定进制
* 转换成boolean时，使用!!
* number去除小数点，使用Math.floor/Math.round/Math.ceil，不使用parseInt

标准库
* 用Number.isNaN代替全局的isNaN
* 用Number.isFinite代替全局的isFinite

注释：
* 注释前使用FIXME或TODO前缀：`// FIXME // TODO`
* 标记:@file、@param、@return、@event、@class、@namespace

空格&空行
* 运算符处换行时，运算符必须在新行的行首
* 在一个代码块后下一条语句前空一行

[链接](http://zero.hikvision.com.cn/#/document/?docId=a8cce7e468a728305f65dc97a2313c66)

