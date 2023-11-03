> TypeScript 的核心设计理念[[6\]](http://ts.xcatliu.com/introduction/what-is-typescript.html#link-6)：在完整保留 JavaScript 运行时行为的基础上，通过引入静态类型系统来提高代码的可维护性，减少可能出现的 bug。

## 对象的类型

### 1. 任意类型

定义接口时，对接口的键名作出限制

1. string  类型

   ```typescript
   interface A {
       [prop : string] : number
   }
   const obj: A = {
       a: 1,
       b: 3,
   };
   ```

2. number 类型

   ```ts
   interface B {
       [index: number] : string
   }
   const arr: B = ['suukii'];
   ```

3. 当同时定义了任意属性和其他属性时，其他属性的键值必须是任意属性的子集

   ```ts
   interface Person {
       name: string;
       age?: number;
       [prop: string]: string;
   }
   // Property 'age' of type 'number' is not assignable to string index type 'string'.
   ```

   



## 函数的类型

### 1.重载

实现根据输入值类型的不同，进行不同操作，并且返回对应类型的值

```ts
function reverse(x: number): number;
function reverse(x: string): string;
function reverse(x: number | string): number | string | void {
    if (typeof x === 'number') {
        return Number(x.toString().split('').reverse().join(''));
    } else if (typeof x === 'string') {
        return x.split('').reverse().join('');
    }
}
console.log(reverse('abc'))
```

