## UI库

**移动端：**

1. mint ui
2. vant
3. cube ui



**pc端：**

1. element ui
2. iview ui



提供定制化打包服务

`npm install babel-plugin-component -D`

 配置babel：

```js
module.exports = {
    presets: [
        "@vue/cli-plugin-babel/preset",
        ["@babel/preset-env", { modules: false }],
    ],
    plugins: [
        [
            "component",
            {
                libraryName: "element-ui",
                styleLibraryName: "theme-chalk",
            },
        ],
    ],
    
};

```

