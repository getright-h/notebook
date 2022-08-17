### 事件绑定

#### 1.on

```js
on('事件',
   //
   [{arg}],
   事件处理函数名)

//上面的事件处理函数
xxx(arg.data){}
```

`on` 可以绑定多个事件

```js
$('div').on({
    click:function({}),
    mouseover:function({})
})
```

`off` 解除綁定

#### 2.事件委托

第二个属性可以为子元素，通过冒泡来批量绑定

```js
$(ul).on('事件',
         'li',
   fn)
```

