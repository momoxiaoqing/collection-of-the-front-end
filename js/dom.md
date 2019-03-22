### childNodes
element.childNodes:包含该元素的所有子元素，不仅仅只有元素节点一种，文档里几乎每一样东西都会解释成节点，比如空格和换行符。


#### nodeType
node.nodeType:共有12种可取值，但仅有3种具有实用价值：

1：元素节点

2：属性节点

3：文本节点


#### nodeValue
node.nodeValue:获取文本内容

node.nodeValue='test' //设置内容

element.nodeValue:null

### firstChild & lastChild
element.firstChild = element.childNodes[0]

element.lastChild

### 修改元素内容
#### add
```
document.createElement(nodeName)
document.createTextNode(test)
```

#### 查找
```
element.nextSibling //下一个兄弟元素
```

#### 更改子元素
```
// 添加、删除子元素
parent.appendChild(node|element);
ele.removeChild(el);

// 替换子元素
ele.replaceChild(el1, el2);

// 插入子元素
parentElement.insertBefore(newElement, targetElement);  //dom不提供insertAfter
```

#### 属性操作
```
// 获取一个{name, value}的数组
var attrs = el.attributes;

// 获取、设置属性
var c = el.getAttribute('class');
el.setAttribute('class', 'highlight');

// 判断、移除属性
el.hasAttribute('class');
el.removeAttribute('class');

// 是否有属性设置
el.hasAttributes();
```

```
element.innerHtml //返回字符串，也可设置元素内容


parent.appendChild(node|element)
parentelement.insertBefore(newElement,targetElement)  //dom不提供insertAfter
element.nextSibling //下一个兄弟元素

element.style //返回object,只返回内嵌样式
```

