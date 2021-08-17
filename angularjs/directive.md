### directive 自定义指令
所有的选项：
```
angular.module('myApp', []).directive('myDirective', function () {
    return {
        restrict: String,
        priority: Number, // 优先级，默认0，ngRepeat是内置指令中优先级最高的，总是最先执行
        terminal: Boolean, //停止运行当前元素上比本指令优先级低的指令，但优先级相同的指令还是会被执行
        template:  String or Template Function:
            function(tElement, tAttrs) (...}, ,
        templateUrl: String,
        replace: Boolean or String,  //默认false
        scope: Boolean or Object,
        transclude: Boolean,  //嵌入，默认false
        controller: String or
                    function($scope, $element, $attrs, $transclude, otherInjectables) { },
        controllerAs: String,
        require: String or Array,
        link: function (scope, iElement, iAttrs) {},
        compile: // 返回一个对象或连接函数，如下所示：
            function (tElement, tAttrs, transclude) {
                return {
                    pre: function (scope, iElement, iAttrs, controller) {
                    }, post: function (scope, iElement, iAttrs, controller) {
                    }
                }
                // 或者
                return function postLink () {
                }
            }
    };
});
```

生命周期：controller --> compile.pre --> compile.post

#### restrict
支持指令使用方式  
* E  //element 标签
* A  //attribute 属性 建议使用，因为有较好的跨浏览器兼容性
* M  //comment 注释
* C  //class 类

#### scope
scope取值：
* false：默认值，指令作用域和父作用域一致
* true：继承父作用域，独立创建作用域
* 对象：隔离作用域，与父作用域完全独立，若需要用父作用域中的属性、方法，需要再scope中添加绑定策略：
  * @：字符串 || 单向绑定 // 单项绑定dom中用{{}}，否则会解析为字符串而非变量
  * = ：双向绑定
  * &：传递函数
  
```
<my-tree naomi="{{naomi}}"></my-tree>  //naomi=naomi.toString()
<my-tree naomi="naomi"></my-tree>  // naomi=‘naomi’

 templateUrl: './tree.html',
  scope: {
      naomi: '@'
  },
```

### transclude 
嵌入通常用来创建可复用的组件，可以将任意内容和作用域传递给指令,类似于vue中的slot  
注意：只当创建一个可以包含任意内容的指令时，才使用transclude: true，此时控制器中无法正常监听数据模型的变化

例子:
```html
<div sidebox title="Links">
    <ul>
        <li>First link</li>
        <li>Second link</li>
    </ul>
</div>
```
```
angular.module('myApp', []).directive('sidebox', function () {
    return {
        restrict: 'EA',
        scope: {title: '@'},
        transclude: true,
        template: `<div class="sidebox">
                       <div class="content">
                            <h2 class="header">{{ title }}</h2>
                            <span class="content" ng-transclude></span>
                        </div>
                    </div>`
    };
});
```

#### replace & transclude
将视图模板（Template或TemplateUrl）替换到指定位置的视图（Restrict） 
* replace:自定义指令名称是否保留。
    * true：不保留指令名
    * false：保留指令名（默认）
* transclude：是否将原来视图的内容嵌入到视图模板（Template或TemplateUrl）中。
    * true：保留替换前的节点内容。
    * false：直接覆盖原有内容。
    * ng-tranclude决定了在什么地方放置嵌入部分。

#### controller
字符串或函数，当设置为字符串时，会以字符串的值为名字， 来查找注册在应用中的控制器的构造函数
```
 controller: function($scope, $element, $attrs, $transclude) { 
         // 控制器逻辑放在这里     
 } })
```
注入的服务有：
* $scope： 与指令元素相关联的当前作用域。
* $element： 当前指令对应的元素
* $attrs： 由当前元素的属性组成的对象
* $transclude ： 嵌入链接函数会与对应的嵌入作用域进行预绑定，是实际被执行用来克隆元素和操作DOM的函数

注意：link函数可以将指令互相隔离开来，而controller则定义可复用的行为

####  controllerAs
用来设置控制器的别名，可以以此为名来发布控制器，并且作用域可以访问controller  
创建匿名控制器：
```
angular.module('myApp').directive('myDirective', function () {
    return {
        restrict: 'A',
        template: '<h4>{{ myController.msg }}</h4>',
        controllerAs: 'myController',
        controller: function () {
            this.msg = "Hello World"
        }
    };
});
```

#### require
require会将控制器注入到其值所指定的指令中，并作为当前指令的链接函数的第四个参数  
require参数的值可以用下面的前缀进行修饰：
* ?：如果在当前指令中没有找到所需要的控制器，会将null作为传给link函数的第四个参数
* ^：指令会在上游的指令链中查找require参数所指定的控制器
* ^?：可选择地加载需要的指令并在父指令链中进行查找
* 无前缀：，指令将会在自身所提供的控制器中进行查找，如果没有找到任何控制器（或 具有指定名字的指令）就抛出一个错误

#### link
link函数创建可以操作DOM的指令，设置事件监听器，监视数据变化和实时的操作DOM  
```
link:function (scope, element,attrs) {
    //  // 在这里操作DOM 
}
```
参数：  
scope参数表示作用域  
element表示指令中的元素，可以通过内置的jqLite调用，jqLite是一个压缩版的jQuery  
attrs参数表示指令元素的属性集合

若指令定义中有require选项，函数签名中会有第四个参数，代表控制器或者所依赖的指令的控制器：
```
// require 'SomeController', 
link: function(scope, element, attrs, SomeController) {   
   // 在这里操作DOM，可以访问required指定的控制器
}
```


#### compile
编译函数负责对模板DOM进行转换，在指令和实时数据被放到DOM中之前，进行DOM操作    
注意：compile和link选项是互斥的。如果同时设置了这两个选项，那么会把compile所返回的函数当作链接函数，而link选项本身则会被忽略

#### 设置默认属性
1、controller中定义属性，用$attrs获取传值，但只能传递string类型的
```
export default angular.module("status", [])
    .controller('statusController', function ($scope, $attrs) {
        $scope.styleType = $attrs.styleType || 'circle'
    }).directive("status", function () {
        return {
            restrict: "EA",
            replace: true,
            scope: {
                statusValue: "=",
                correctName: "=",
                errorName: "="
            },
            template: require('./index.html'),
            controller: 'statusController'
        }
    }).name
```
或者：
```
export default angular.module("status", [])
    .directive("status", function () {
        return {
            restrict: "EA",
            replace: true,
            scope: {
                statusValue: "=",
                correctName: "=",
                errorName: "="
            },
            template: require('./index.html'),
            controller: function ($scope, $attrs) {
                $scope.styleType = $attrs.styleType || 'circle'
            }
        }
    }).name
```

2、scope中用'=?'定义，可以传递其他类型的值：
```
export default angular.module("status", [])
    .directive("status", function () {
        return {
            restrict: "EA",
            replace: true,
            scope: {
                statusValue: "=",
                correctName: "=",
                errorName: "=",
                styleType:'=?'
            },
            template: require('./index.html'),
            controller: function ($scope) {
                $scope.styleType = $scope.styleType || 'circle'
            }
        }
    }).name
```
