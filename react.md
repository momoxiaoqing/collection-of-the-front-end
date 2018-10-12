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





