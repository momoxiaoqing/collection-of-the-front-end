### map（映射）
Object 结构提供了“字符串—值”的对应，Map 结构提供了“值—值”的对应，健不一定是字符串  
保存键值对，并且能够记住键的原始插入顺序

#### 语法：
```
new Map()
map.size
```

#### 方法：
* clear()
* get(key)
* set(key, value)
* delete(key)
* has(key)
* keys() //按顺序返回key
* values() //按顺序返回value
* entries()
* forEach(callbackFn[, thisArg])

#### 迭代
1、for..of
```javascript
for (let [key, value] of myMap) {
  console.log(key + " = " + value);
}
```

2、forEach()
```javascript
myMap.forEach(function(value, key) {
  console.log(key + " = " + value);
})
```

### set（集合）
类似数组，但成员的值都是唯一的，没有重复的值。



### map VS object
|     |  map   |  object | 
|  ----   | ----  |  ----  |
| 意外的key | 无 |  可能包含原型链上的key |
| key类型   | 任意值 |  String 或是Symbol |
| key顺序   | 有序 |  无序 |
| size   | map.size |  手动计算 |
| 迭代   | 可迭代 |  需要通过key迭代 |
| 性能   | 在频繁增删键值对的场景下表现更好 |   |
