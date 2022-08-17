## AJAX

47.109.16.231.3000/login/getuser

### 1.基本

```js
$.ajax({
    url:'xx.xx.xx.xx:3000/login/getuser',//请求地址
    type:'get' | 'post',//请求方式
    data:{
        //json对象
        username:'xx',
        password:'xx',
        type:'',
        
    },
    {
    success:function(data){
    //返回的是data对象
    console.log(data.data)
}
}
})
```

```js
$.ajax({
  url: 'time.php',
  type: 'get',
  beforeSend: function (xhr) {
    // 在所有发送请求的操作（open, send）之前执行
    console.log('beforeSend', xhr)
  },
  success: function (res) {
    // 隐藏 loading
    // 只有请求成功（状态码为200）才会执行这个函数
    console.log(res)
  },
  error: function (xhr) {
    // 隐藏 loading
    // 只有请求不正常（状态码不为200）才会执行
    console.log('error', xhr)
  },
  complete: function (xhr) {
    // 不管是成功还是失败都是完成，都会执行这个 complete 函数
    console.log('complete', xhr)
  }
})
```



**全局**

```js
  $(document)
  .ajaxStart(function () {
    // 只要有 ajax 请求发生 就会执行
    $('.loading').fadeIn()
    // 显示加载提示
    console.log('注意即将要开始请求了')
  })
  .ajaxStop(function () {
    // 只要有 ajax 请求结束 就会执行
    $('.loading').fadeOut()
    // 结束提示
    console.log('请求结束了')
  })

$('#btn').on('click', function () {
  // $.ajax({
  //   url: 'time.php'
  // })

  $.get('time.php')
})
```



### 2.token

- `token`存活期为本地存储，
- `session` 浏览器存续时间
- `cokkie`页面存续时间
- `localStorage.setItem('键','值')` 本地存储只能存字符串，布尔值需要手动转换
  - 可以先把对象转换成字符串`JSON.stringify()`
  - `JSON.parse` 字符串回到对象

