### 垂直居中
* 绝对定位 + top50% +负外边距(margin用%时，不用知道被居中块的高度)
```
     #box {
         width: 300px;
         height: 300px;
         background: #ddd;
         position: relative;
     }
     #child {
         width: 50%;
         height: 30%;
         background: orange;
         position: absolute;
         top: 50%;
         margin: -15% 0 0 0;
}

```

* 绝对定位 + transform ：translate偏移的%是相对元素自身的
```
    #child {
            width: 150px;
            height: 100px;
            background: orange;
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
        }
```