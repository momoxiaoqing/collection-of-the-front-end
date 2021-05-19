### 过滤器

### 串联
```vue
{{ message | filterA | filterB }}
```

#### 传参
```vue
{{ message | filterA('arg1', arg2) }}
```

### js调用方式
```vue
<div v-html="$options.filters.formatRate(value,'arg1')"></div>
```