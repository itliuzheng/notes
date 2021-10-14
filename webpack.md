## 常用插件

### 1. DefinePlugin

```javascript
new webpack.DefinePlugin({
    VERSION: JSON.stringify('1.0.0'),
    BOR:true,
    TWO:1+1
})

//带编译文件
console.log(VERSION);  //1.0.0
```



###　２.ProvidePlugin

```javascript
new webpack.ProvidePlugin({
    $:'jquery'
})
```

