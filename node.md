起步：[https://github.com/nswbmw/N-blog](https://github.com/nswbmw/N-blog)

### 项目内使用2个模板

```
//.html引用art模板，.ejs引用ejs模板
//如res.render('index.html'）引用art模板，res.render('index.ejs'）引用ejs模板，
app.engine('html', require('express-art-template'));
app.set('view engine', 'html');
app.set("views", path.resolve(__dirname, "views"));
app.engine("ejs", ejs.renderFile);

```



