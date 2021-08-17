### 服务

#### $watch
第三个参数用于告诉Angular，是否使用深度比较来监控这个对象，它会使用angular.equals()函数检查每个属性
```
 var unWatch = $scope.$watch(attrs.name, function(newvalue, oldValue) {
     if(n != o) { 
         // 使用解析后的name做些什么事
         // 然后移除watch      
         unWatch(); 
     }             
 },isDeepWatch); 
```