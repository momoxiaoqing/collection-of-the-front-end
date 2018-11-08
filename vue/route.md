### 路由嵌套

```js
      {
            path: '/survey/:surveyId/paper',
            name: 'paper',
            component: paper,
            children: [
                {
                    path: '',
                    name: 'questionSubject',
                    component: questionSubject
                },
                {
                    path: 'question-list',
                    name: 'questionList',
                    component: questionList
                }
            ]
        },
```

使用时直接{name:'questionSubject‘}，而不是{name:'paper’}，否则会出现路由跳转时不加载questionSubject，刷新时才会加载的现象

### 



