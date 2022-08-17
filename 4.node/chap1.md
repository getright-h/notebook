## NODEJS

**目录操作:**

`cd`进入下级目录

`cd ../`返回上级



#### issue：

1. 使用cnpm install时候，并**不会生成**package-lock.json文件
2. 暴露 `module.exports = {}`,引入 `require('')`



#### 1.服务搭建

**express脚手架：**

-dev 项目开发依赖,上线就不需要了

-save 项目依赖，开发，项目都需要

-g 全局

```js
npm i express-generator -g
express node-project

npm install	//下载对应依赖
npm install mysql	//mysql依赖
```

下载依赖包，根据package.json来下载





#### 2.路由分发

`req.query` get

`req.body` post



#### 3.config文件夹

配置数据库文件





```js
/* 
  1.拿到请求数据
  req.query 数据

  2.发送给数据库
    2.1获取数据库对象(要安装依赖包)
      2.1.1引入mysql包,(依赖)
      2.1.2创建对象
      let database = mysql.creatConnection({
        host:'localhost',
        port:'3306',
        user:'root',
        password:'123',
        database:'xxx'
      })
    2.2连接数据库
      database.connect()
    2.3操作数据库
    database.query(sql,值,操作数据库完毕后执行的函数)
      //? 占位
    database.query(
      'select * from xx where x = ?',[传入?的变量],
      function(err,data){
        //使用数据，进行操作

        //成功，发送
        res.send('')
      }
    )
    2.4关闭数据库
    database.end()

  3.根据结果返回给浏览器
  */
```





## ajax

异步请求，局部刷新

#### 1.获取ajax对象

在打开对象和发起请求之间，要设置**请求头**

**请求类型：**

`get`

`post`在打开对象和发起请求之间，要设置**请求头**

```js
xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded'); 
```



判断是否为ie

```js
if(window.XMLHttpRequest){
    let xhr = new XMLHttpRequest()
    }else{
        let xhr = new ActiveXObject('Microsoft.XMLHTTP')
    }
```



#### 2.打开ajax对象

`布尔值`同步false/异步true，默认异步

```js
xhr.open(请求方式，请求地址?get的参数值，布尔值)
```



#### 3.设置事件处理函数

`xhr.readyState`:

0,请求没初始化

1，服务已连接，正在发送请求

2，请求已经接受 

3，请求处理中，正在解析响应内容

4，请求已完成，响应已就绪

`xhr.status === 200`

```js
xhr.onreadyStateChange = function(){
    //请求之后要干的事情
    //判断
    //xhr.readyState:0 ,1,2,3,4
    //xhr.status
   	//succsee
    //获取返回数据，转为js对象
    JSON.parse(xhr.responseText)
    xhr.responseText
}
```



#### 4.发送请求

```js
xhr.send()
```

