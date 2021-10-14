```javascript
//router.js
//解决使用路由重定向做了登录验证后, 报错
//Error: Redirected from “/login” to “/index” via a navigation guard.

const originalPush = Router.prototype.push;
Router.prototype.push = function push (location, onResolve, onReject) {
  if (onResolve || onReject) return originalPush.call(this, location, onResolve, onReject)
  return originalPush.call(this, location).catch(err => err)
}
```



## vue2.0

### 新增指令

#### 1.v-once

表明该元素是一个静态根节点，这些节点生成后内容就不会被改变，因此在Virtual DOM的diff和patch的过程中，可以忽略这些节点来提升性能







