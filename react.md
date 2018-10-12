### 一、生命周期图解

![](/assets/832416858-5b077e7f0fcd7_articlex.png)

### 二、state

1、不要直接修改status

```
// Wrong
this.state.comment = 'Hello';

// Correct
this.setState({comment: 'Hello'});
```

2、`this.props`和`this.state`可能是异步更新的，你不应该依靠它们的值来计算下一个状态。

```
// Wrong
this.setState({
  counter: this.state.counter + this.props.increment,
});

// Correct
this.setState((prevState, props) => ({
  counter: prevState.counter + props.increment
}));
```



