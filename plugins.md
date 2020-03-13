### 插件间的冲突
#### echarts4.x.x && swiper4.x.x
echarts.on点击事件会监听失效
```
 chart.on('click', function (params) {

 });
```

亲测：echarts4.1.1、4.2.0、4.2.1 + swiper4.5.0 失效

解决方法：echarts4.x.x + swiper3.x.x 或者 echarts3.x.x + swiper4.x.x无冲突

亲测：
* echarts4.1.1、4.2.0、4.2.1 + swiper3.4.2 无冲突
* echarts3.1.10 + swiper4.5.0 无冲突