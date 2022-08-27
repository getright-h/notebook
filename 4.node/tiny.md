1. app.js注释掉这段，快要提示报错

   ```js
   // error handler
   app.use(function (err, req, res, next) {
       // set locals, only providing error in development
       res.locals.message = err.message;
       res.locals.error =
           req.app.get("env") === "development" ? err : {};
   
       // render the error page
       res.status(err.status || 500);
       res.render("error");
   });
   ```

2. 

下面给大家介绍一种方法可以快速删除node_modules，让你彻底告别这个苦恼。。。

```undefined
npm install rimraf -g
rimraf node_modules
```

或者

```undefined
rmdir /s/q node_modules
```

删除文件

```python
del filename
```

清除node_modules缓存

```undefined
npm cache clean
```

