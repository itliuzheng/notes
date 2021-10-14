# UnhandledPromiseRejectionWarning: #<Object>

```javascript
UnhandledPromiseRejectionWarning: #<Object>

如果你定义的Promise没有进行Catch处理Rejection这种情况，就会有这个提示，解决方法有几个：
1.直接用resolve来返回错误代码而不用reject
2.直接在Promise里用空函数处理
new Promise().catch(()=>{})
3.用node process的全局unhandledRejection事件来处理
process.on('unhandledRejection',err=>{
    console.log(err);
})
注意，这种情况下，全局的unhandledRejection事件会优先处理这个错误，也就是像第二种在Promise里用Catch处理是不会生效的。
```

