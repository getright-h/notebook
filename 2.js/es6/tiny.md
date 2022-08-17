#### 1.函数参数默认值

```js
function connet({ host = "127.0.0.1", username, password, port }) {
    console.log(host, username, password, port);
}						
connet({
    // host: "",
    username: "root",
    password: "123",
    port: "80",
});

```

#### 2.



#### 一些面试题

1. 一个函数中，当变量和参数名字重复时
   1. 变量没有赋值，该命名由参数使用
   2. 变量赋值了，该命名由变量使用
2. 严格模式中
   1. 不能在if else 中定义函数
   2. 全局中的this 指向undefined 而非 window
   3. 禁用 eval