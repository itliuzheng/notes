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









