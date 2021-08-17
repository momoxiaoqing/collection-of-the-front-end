### controller

#### scope 作用域
$scope对象的职责是承载DOM中指令所共享的操作和模型  
* 操作指的是$scope上的标准JavaScript方法
* 模型指的是$scope上保存的包含瞬时状态数据的JavaScript对象。持久化状态的数据应该保存到服务中，服务的作用是处理模型的持久化。
* 绝对不要直接将控制器中的$scope赋值为值类型、对象（字符串、布尔值或数字）
* 控制器应尽可能简单。建议将业务逻辑放在移到服务和指令中

#### 父子控制器
子控制器继承父控制器变量，若为引用类型则是引用赋值，否则就是值赋值  
推荐用引用类型
```
<div ng-controller="SomeController"> {{ someModel.someValue }}
    <button ng-click="someAction()">Communicate to child</button>
    <div ng-controller="ChildController"> {{ someModel.someValue }}
        <button ng-click="childAction()">Communicate to parent</button>
    </div>
</div>

// 父会影响子，子不会影响父
angular.module('myApp', []).controller('SomeController', function ($scope) {
       $scope.someBareValue = 'hello computer';
       $scope.someAction = function () {
           $scope.someBareValue = 'hello human, from parent';
       };
   }).controller('ChildController', function ($scope) {
       $scope.childAction = function () {
           $scope.someBareValue = 'hello human, from child';
   };
});

// 父子共享变量，引用赋值
angular.module('myApp', []).controller('SomeController', function ($scope) {
    $scope.someModel = {someValue: 'hello computer'}
    $scope.someAction = function () {
        $scope.someModel.someValue = 'hello human, from parent';
    };
}).controller('ChildController', function ($scope) {
    $scope.childAction = function () {
        $scope.someModel.someValue = 'hello human, from child';
    };
});   
```

