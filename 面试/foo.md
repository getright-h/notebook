# JS

## this

### 1. null

`call(null,undefined)` this返回window

### 2. 对象中函数的this

```js
var obj = {
   say: function() {
     var f1 = () =>  {
       console.log("1111", this);
     }
     f1();
   },
   pro: {
     getPro:() =>  {
        console.log(this);
     }
   }
}
var o = obj.say;
o(); //window
obj.say();//obj
obj.pro.getPro();//window
```

1. `f1`是箭头函数，其this指向父级的this，父函数`say`在window中调用，所以是window
2. 调用是`obj`，this指向obj
3. 同理`getPro`向上级查询this，但是上级是一个对象，对象不创建单独的作用域，所以指向了window



### 3. 立即执行函数的this

```js
var myObject = {
    foo: "bar",
    func: function() {
        var self = this;
        console.log(this.foo);  
        console.log(self.foo);  
        (function() {
            console.log(this.foo);  
            console.log(self.foo);  
        }());
    }
};
myObject.func();
// bar bar undefined bar
```

立即指向函数的this总是指向window

立即执行函数会向上查找作用域链中的属性

### 4. arguments调用的this

```js
var length = 10;
function fn () {
    console.log(this.length);
}

var obj = {
    length: 5,
    method: function (qw) {
        qw();//10
        arguments[0]();//2
    }
};

obj.method(fn, 1);
```

通过`arguments`调用this，指向函数的活动对象，活动对象是函数在调用时创建的，该活动对象会被插入到作用域链中







## 作用域

### 1.函数中的变量提升

会把var function提升到当前作用域的顶部

```js
var friendName = 'World';
(function() {
  if (typeof friendName === 'undefined') {
    var friendName = 'Jack';
    console.log('Goodbye ' + friendName);
  } else {
    console.log('Hello ' + friendName);
  }
})();
--相当于--
var name = 'World!';
(function () {
    var name;
    if (typeof name === 'undefined') {
        name = 'Jack';
        console.log('Goodbye ' + name);
    } else {
        console.log('Hello ' + name);
    }
})();
```

### 2. 函数的作用域

函数在定义的时候作用域能访问的属性就确定了，

这里定义在window环境中，调用函数时生成的作用域链中只有window和其本身的属性

```js
var a = 3;
function c () {
    alert(a);
}
function b () {
    var a = 4;
    c();
}
b()
```

### 3. 离谱

```js
function fun (n, o) {
    console.log(o)
    return {
        fun: function (m) {
            return fun(m, n);
        }
    };
}
var a = fun(0); a.fun(1); a.fun(2); a.fun(3);
var b = fun(0).fun(1).fun(2).fun(3);
var c = fun(0).fun(1); c.fun(2); c.fun(3);
```



## 原型

```js
function Person (name) {
    this.name = name
}
var p2 = new Person('king');
```



**实例的constructor始终指向创建当前对象的构造函数。** `console.log(p2.constructor)//Person`

**函数的原型的constructor指向该函数本身** `console.log(Person.prototype.constructor)//Person`

