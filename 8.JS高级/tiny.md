1. **声明式函数**有变量提升，**函数表达式**没有提升

   ```js
   bar(){}//声明
   var foo = function(){}//表达式
   ```

2. 连等赋值

   ```js
   var a=b=c=1;
   //相当于
   var a
   c=1
   b=c
   a=b
   
   ```

3. 函数默认参数

   ```js
   function foo (n){
       //判断有无传参数
       if(n = n|| 10)
   }
   
   //es6 有就不传，没就传10
   function foo(n = 10){}
   ```

4. 逻辑中断

   1. `&&`返回fasle那项，全false取后者

      ```js
      let a = 3 > 5;
      let b = 1 == 1;
      console.log(a && b);
      
      ```

   2. `||`返回true那项，全true取后者

      ```js
      let a = 3 > 5;
      let b = 1 == 1;
      console.log(a && b);
      
      ```

5. 数组的扩展方法

   1. keys() 返回键名
   2. values() 键值
   3. entries() 键值对

   ```js
   for (let index of ['a', 'b'].keys()) {
     console.log(index);
   }
   // 0
   // 1
   
   for (let elem of ['a', 'b'].values()) {
     console.log(elem);
   }
   // 'a'
   // 'b'
   
   for (let [index, elem] of ['a', 'b'].entries()) {
     console.log(index, elem);
   }
   // 0 "a"
   // 1 "b"
   ```

6. Map 数据类型

   键值，可以为任意数据类型(传统键名只能是string，symbol，数字)

   ```js
   let key = {name : 'xx'}
   let value = {age:12}
   let arr = new Map()
   arr.set(key,value)
   ```

   ```js
   arr.set()
   .get()
   .has()
   .delete()
   .clear() //清除所有
   ```

7. set 数据类型

   数组去重，返回去重后的数组，也是任意数据类型都可以当键名

   ```js
   // 去除数组的重复成员
   [...new Set(array)]
   ```

   



