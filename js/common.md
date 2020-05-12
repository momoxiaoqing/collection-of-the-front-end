### 常用方法
1、多行省略号，默认```<div class="short-div"><p></p></div>```结构
```
function wordLimit (divStr) {
    divStr=divStr||'.short-div';
    $(divStr).each(function () {
        var divH = $(this).height();
        // var p = pStr || "p";
        // var $p = $(p, $(this));
        var $p = $(this).children();
        var isOver = 0;
        while (divH < $p.height()) {
            isOver = 1;
            $p.html($p.html().replace(/((\s)*([a-zA-Z0-9]+|\W)(\.\.\.)?){20}$/, "..."));
        }
        if (isOver) {
            // $p.html($p.html().replace(/((\s)*([a-zA-Z0-9]+|\W)(\.\.\.)?){5}$/, "..."));
        }
    });
}
```

2、获取search关键字
```
function getParamFromSearch (key, type) {
       type = type || 'search';
       var value = null;
       var search = window.location[type];
       if (search) {
           search = search.substring(1).split("&")
           var item;
           for (var i = 0, len = search.length; i < len; i++) {
               item = search[i].split('=');
               if (item && item[0] == key) {
                   value = decodeURIComponent(item[1]);
                   break;
               }
           }
       }
       return value
   }
```


3、获取页面名字
```
function getPageName (url) {
    url=url||window.location.href;
    var pageName=/\/(\w+\-*\w*\-*\w*)\.html/.exec(url);
    return pageName!==null?pageName[pageName.length-1]:null
}
```

4、获取即将跳转页面地址
```
function getFrontUrl (key) {
    var url=getPageName()+'.html?';
    var search=location.search;
    if(search){
        search=search.slice(1).split('&');
        if(search.length>0){
            for(var i=0,len=search.length;i<len;i++){
                var item=search[i].split('=');
                if(item[0]!==key){
                    url+=search[i];
                }
            }
            url+='&'
        }
    }
    url+=key+'=';
    return url;
}
```