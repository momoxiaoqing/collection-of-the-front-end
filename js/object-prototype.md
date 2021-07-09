### 原型 & 原型链
![](/assets/prototype.png)  
原型链是蓝色线

```js
function Person() {
}
var person = new Person();
console.log(person.__proto__ === Person.prototype); // true 
console.log(Person === Person.prototype.constructor); // true
console.log(Object.prototype.__proto__ === null) // true
```

从对象中找不到属性就会从原型中查找：
```js
function Person() {

}

Person.prototype.name = 'Kevin';

var person = new Person();

person.name = 'Daisy';
console.log(person.name) // Daisy

delete person.name;
console.log(person.name) // Kevin
```

注意：
* __proto__：使用__proto__时，可以理解为返回Object.getPrototypeOf(obj)