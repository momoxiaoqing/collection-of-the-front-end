### appearance
用来设计拥有平台原生UI样式的自定义的组件
* -moz-appearance : none;  //Firefox（Gecko）
* -webkit-appearance : none;  //Chrome, Opera,Safari（Blink ）

值：
* none
* button
* checkbox
*  ....
[MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/appearance)

#### 修改input、select等样式
[伪元素-表单样式](https://www.zhangxinxu.com/wordpress/2013/06/伪元素-表单样式-pseudo-elements-style-form-controls/)

##### input[type=date]:
```
input[type="date"]::-webkit-calendar-picker-indicator,
input[type="date"]::-webkit-clear-button
```
以上设置在Safari中会影响日期控件的打开，延迟响应

##### select
```
 <div class="select-div">
     <select name="compare" class="date-type home-fruit">
         <option value="com">周同比</option>
         <option value="com">月同比</option>
         <option value="com">季同比</option>
         <option value="com">周环比</option>
         <option value="com">月环比</option>
     </select>
 </div>

 .date-input,
 .date-type{
     height: 30px;
     padding: 0 5px;
     line-height: 24px;
     appearance: none;
     -moz-appearance: none;
     -webkit-appearance:none;
     text-align: center;
 }
 .select-div{
     position: relative;
     padding-right: 2rem;
 }
 .select-div:after{
     position: absolute;
     top: 50%;
     transform: translateY(-0.2rem);
     right: 5px;
     border-width: 0.5rem 0.3rem;
     border-style: solid;
     content: '';
     z-index: 99;
      border-color: #ecca8b transparent transparent transparent;
 }
 select,
 .select-div{
   background-color: #fffbf0;
   color: #f0af51;
 }
```