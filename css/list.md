### css属性作用记录
* backdrop-filter //背景模糊，本身需有透明度
* filter //自身模糊


backdrop-filter 兼容性写法
```css
.some-class-zxx {
    background-color: #fff;  
}
@supports (-webkit-backdrop-filter:none) or (backdrop-filter:none) {
    .some-class-zxx {
        background: hsla(0, 0%, 100%, .75); 
        -webkit-backdrop-filter: blur(5px);    
        backdrop-filter: blur(5px);   
    }
}
```