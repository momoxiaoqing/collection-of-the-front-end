### [super](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/super)
用于访问和调用一个对象的父对象上的函数

用法：
```
super([arguments]);
// 调用 父对象/父类 的构造函数

super.functionOnParent([arguments]);
// 调用 父对象/父类 上的方法
```

注意：
* 在构造函数中，super必须用于this之前
* 不能删除，否则将抛异常
* 不能覆写不可写属性：当使用 Object.defineProperty 定义一个属性为不可写时，super将不能重写这个属性的值。


#### 例子
super([arguments])
```
class Polygon {
    constructor(height, width) {
        this.name = 'Polygon';
        this.height = 1;
        this.width = 1;
    }
}

class Square extends Polygon {
    constructor(width,height) {
        this.height;
        this.name = 'Square';
    }

```

super.functionOnParent([arguments])
```
class Rectangle {
    constructor() {}
    static logNbSides() {
        return 'I have 4 sides';
    }
}

class Square extends Rectangle {
    constructor() {}
    static logDescription() {
        return super.logNbSides() + ' which are all equal';
    }
}
```

