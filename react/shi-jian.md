1、命名：驼峰式

2、语法：

```js
<button onClick={activateLasers}>
  Activate Lasers
</button>
```

3、不能返回false 来阻止默认行为，必须用preventDefault

```js
function handleClick(e) {
    e.preventDefault();
    console.log('The link was clicked.');
  }
```





