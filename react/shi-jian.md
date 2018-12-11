### 一、基础

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

### 二、绑定

类的方法默认是不会绑定 this 的，需要绑定。

建议：

1、在构造函数中绑定

2、使用属性初始化器语法

5、事件中有无()区别：

简单点说，带括号的是函数调用，直接执行函数；不带括号的是绑定事件，事件触发再执行。

复杂点说，带括号的是把返回值赋值给事件，不带括号的是把函数体所在地址位置赋值给事件。

```js
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8"/>
    <title>Hello World</title>
    <script src="https://unpkg.com/react@16/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>

    <!-- Don't use this in production: -->
    <script src="https://unpkg.com/babel-standalone@6.15.0/babel.min.js"></script>
</head>
<body>
<div id="root"></div>
<script type="text/babel">
    class Clock extends React.Component {
        constructor (props) {
            super(props);
            this.state = {
                date: new Date(),
                posts: [1],
                comments: [1],
                count:1
            };
            this.add=this.add.bind(this) //将add方法绑定到this上；
        }

        //当组件输出到 DOM 后会执行
        componentDidMount () {
            this.timerID = setInterval(() => this.tick(), 1000)
        }

        //卸载计时器：
        componentWillUnmount () {
            clearInterval(this.timerID)
        }

        tick(){
            this.setState({
                date:new Date(),
                posts:[1,2,3]
            })
        }
        add(){
            this.setState((prevState)=>{
                debugger
                count:prevState.count++
            })
        }
        render () {
            return (
                <div>
                    <div>{this.state.count}</div>
                    <div><button onClick={this.add}>add</button></div>
                    //<div><button onClick={(e)=>this.add(e)}>add</button></div> //无须绑定
                    //<div><button onClick={this.add()}>add</button></div>  //不管是否绑定add方法，count会随date变化
                    <div>
                        <h1>Hello world !</h1>
                        <h2>It is {this.state.date.toLocaleTimeString()}</h2>
                        <h2>{this.state.posts}</h2>
                        <h2>{this.state.comments}</h2>
                    </div>
                </div>
            )
        }
    }

    ReactDOM.render(
        <Clock/>,
        document.getElementById('root')
    );


</script>
</body>
</html>
```



