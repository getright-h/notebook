### 1.前后端路由衔接 debug(思路)：

1. 400，500 首先确定路由拦截有没有拦截(前端请求有没有发起)，确定前端数据有没有拿到

   1. 前端的错误  

      1. 数据有没有获取到

      2. 发送的数据是不是和js获取的一样

         console.log(发送的data)

   2. 后端错误

      1. 有可能需要一次请求多次操作，但node操作数据库是异步，所有需要promise
      2. 确认前端数据有没有接收到(get query ,post body)
      3. 业务逻辑梳理







