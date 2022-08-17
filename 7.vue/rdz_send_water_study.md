## index

### 1.高度 自适应 

#### 1.1固定的侧边栏

```cs
.aside{
    height:calc(100vh - 头部的高度px)
}
```

#### 1.2自适应的容器

通过监听事件 `resize`, 来获取当前页面 **视窗** 的高度`window.document.documentElement.clientHeight` 

并把每次变换后的高度存放在vuex中，

这样就可以让容器 根据页面大小，重新计算其高度了

````js
window.addEventListener("resize", this.setTableHeight);

setTableHeight() {
    const height = window.document.documentElement.clientHeight;
    this.$store.dispatch("setTableHeight", height);
},
    //container
    tableHeight() {
        return this.$store.getters.tableHeight - 245;
    },
````

### 2.侧边栏路由跳转

```js
//路由
goRouter(name) {
    const path = `/index/${name}`;
    this.$router.push(path);
},
    //组件
    -----------------
        <el-menu-item
    :index="item.name"
style="text-align: left"
v-for="item in menulist"
:key="item.id"
@click="goRouter(item.name)"
>
    ------------------
// 菜单列表
menulist: [
    {
        label: "领取详单",
        name: "receiveOrder",
        id: "1",
        icon: "m-icon el-icon-document-checked",
    },
    {
        label: "领取报表",
        name: "receiveReport",
        id: "2",
        icon: "m-icon el-icon-tickets",
    },
],
```

## 共用组件

### 1.深拷贝，重写需要展示的数据

```js
//克隆需要重写的数据
let list = CLONEDEEP(this.list)
//重写
ele.list = ele.list.map(el => ({ label: el[ele.key], value: el[ele.value] }))
```



## vue.config.js

###  1.生产环境去掉console.log

```js
configureWebpack: (config) => {

    if (process.env.NODE_ENV === 'production') {

        config.optimization.minimizer[0].options.terserOptions.compress.drop_console = true

    }

}
```

