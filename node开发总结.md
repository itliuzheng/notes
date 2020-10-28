## node

### path 路径操作模块

- path.basename
  - 获取一个路径的文件名（默认包含扩展名）
- path.dirname
  - 获取一个路径中的目录部分
- path.extname
  - 获取一个路径中的扩展名部分
- path.parse
  - 把一个路径转为对象
    - root 	根路径
    - dir        目录
    - base     包含后缀名的文件名
    - ext        后缀名
    - name   不包含后缀名的文件名
- path.join
  - 当你需要进行路径拼接的时候，推荐使这个方法
- path.resolve
  - 把一个路径或路径片段的序列解析为一个绝对路径。相当于执行cd操作。
- path.isAbsolute
  - 判断一个路径是否是绝对路径

```javascript
//path.relative() 方法根据当前工作目录返回 from 到 to 的相对路径。 如果 from 和 to 各自解析到相同的路径（分别调用 path.resolve() 之后），则返回零长度的字符串。

path.relative('/data/orandea/test/aaa', '/data/orandea/impl/bbb');
// 返回: '../../impl/bbb'
```



### fs 文件模块

```javascript
fs.existsSync('路径')
//如果路径存在，则返回 true，否则返回 false。

fs.mkdirSync('路径')
//同步地创建目录。 返回 undefined

fs.renameSync(oldPath, newPath)
//同步地rename。 返回 undefined

fs.rename(oldPath, newPath, callback)
//异步地把 oldPath 文件重命名为 newPath 提供的路径名。 如果 newPath 已存在，则覆盖它。 除了可能的异常，完成回调没有其他参数。
```

### node中的非模块成员（其他成员）  

在每个模块中，除了 `require`、`exports`等模块相关API之外，还有两个特殊的成员

- `__dirname` 	**动态获取 **  可以用来获取当前文件模块所属目录的绝对路径
- `__filename`   **动态获取 **  可以用来获取当前文件的绝对路径
- `__dirname`和`__filename`是不受执行node命令所属路径影响的

在文件操作中，使用相对路径是不可靠的，因为在Node中文件操作的路径被设计为相对于执行node命令所处的路径。

所以为了解决问题，只需要把   **相对路径**   改为   动态的  **绝对路径**

使用 `__dirname` 或者 `__filename`  来解决这个问题

在拼接路径的过程中，为了避免手动拼接带来的低级错误，推荐使用 `path.join()`来辅助拼接

在文件操作中使用的相对路径都统一转换为 **动态的绝对路径**

`>`

> 补充，模块中的路径表示和这里的文件路径没关系，
>
> 模块中的路径标识和文件操作中的相对路径标识不一致
>
> `require('./b.js')`       模块中的路径标识就是相对于当前文件模块，不受执行node命令所处路径影响
>
> `fs.readFile('./b.js')`

### 错误相关问题

```javascript
Error: EXDEV: cross-device link not permitted, rename 'C：/xxx' -> 'D:/xxx'

//文件上传的功能时候，调用fs.renameSync方法错误
//这个提示是跨区重命名文件出现的权限问题。

//解决问题
let form = new formidable.IncomingForm();
form.uploadDir = vacationPhotoDir; //设置上传目录

```

### nodejs命令行执行时带参数

```javascript
/*
//node test.js arg1 arg2 arg3， 想取得这三个参数
//即可以程序中用：
	var args = process.argv.splice(2)
//process是一个全局对象，argv返回的是一组包含命令行参数的数组。
//第一项为”node”，第二项为执行的js的完整路径，后面是附加在命令行后的参数
*/
```

### nodejs执行cmd命令

```javascript
const { execSync } = require('child_process');
const path = require('path')
const fs = require('fs')

function runSync(code) {
    console.log(code);
    execSync(code,{
        cwd:path.resolve(__dirname,'./backend'),
        encoding:'utf8',
        maxBuffer: 1024 * 2000
    });
}

let arguments = process.argv.splice(2)
console.log(arguments);

if(arguments && arguments[0] == 'build'){
    runSync('npm run build')
}

if(fs.existsSync(path.resolve(__dirname,'./views/_admin'))){
    console.log('该路径已存在');
    runSync(`rmdir /s/q ${path.resolve(__dirname,'./views/_admin')}`)
    runSync(`mkdir ${path.resolve(__dirname,'./views/_admin')}`)
    runSync(`mkdir ${path.resolve(__dirname,'./views/_admin/static')}`)
}else{
    console.log('该路径不存在');
    runSync(`mkdir ${path.resolve(__dirname,'./views/_admin')}`)
    runSync(`mkdir ${path.resolve(__dirname,'./views/_admin/static')}`)
}

runSync(`copy ${path.resolve(__dirname,'./backend/dist/index.html')} ${path.resolve(__dirname,'./views/_admin')}`)
runSync(`xcopy ${path.resolve(__dirname,'./backend/dist/static')} ${path.resolve(__dirname,'./views/_admin/static')} /s /f /h`)


```





## Express

### 配置 `art-template`模板引擎

#### art-template模板引擎

##### 模板命令及基础用法

```html

<!-- if -->
{{if xxx>19}}
{{else if xxx>15}}
{{else}}
{{/if}}

<!-- 循环 -->
{{each xxx}}
	{{$value}}
{{/each}}

<!-- 引入子模版 -->
{{ include './xxx.html'}}

<!-- 模版继承 -->
{{ extend './xxx.html'}}
```

##### 模板引擎循环嵌套问题

```bash
{{each object  value   index }}
```

##### 

### 在Express中获取表单GET请求参数

### 在Express中获取表单POST请求体数据

```shell
npm install --save body-parser
```



```javascript
var bodyParser = require('body-parser')

app.use(bodyParser.urlencoded({extended:false}))
app.use(bodyParser.json())
```



### 跨域问题解决

```shell
npm install --save cors
```



```javascript
var CORS = require('cors');

//解决跨域问题
app.use(CORS({
    origin:['http://localhost:8080'],
    methods:['GET','POST']
}))
//跨域问题解决方面
app.all('*',function(req,res,next) {
    res.header('Access-Control-Allow-Origin','http://localhost:8080');
    res.header('Access-Control-Allow-Headers','Content-Type');
    res.header('Access-Control-Allow-Methods','PUT,POST,GET,DELETE,OPTIONS');
    next();
})
```



### 在Express配置使用`express-session`插件

[^参考文档]: https://github.com/expressjs/session

#### 安装

```shell
npm install --save express-session
```

#### 配置

```javascript
/**
 *  该插件会为req 请求对象添加一个成员  req.session默认是一个对象
 *  req.session 来访问和设置session成员
 */
app.use(session({
    secret:'node test',   //加密字符串   增加安全性
    resave:false,
    saveUninitialized:false  //无论你是否使用Session，我都默认直接给你分配一把钥匙
}))
```

#### 使用

```javascript
//添加成员
req.session.xxx = 'xxx'  

//访问数据
req.session.xxx  
```

**提示**: 默认Session数据是内存存储的，服务器一旦重启就会丢失。真正的生产环境会把Session进行持久化存储。

### Token验证实现方案

#### 什么是Token

在计算机身份认证中是令牌（临时）的意思，

在词法分析中是标记的意思。

一般我们所说的的token大多是指用于身份验证的token

#### Token的特点

1. 随机性
2. 不可预测性
3. 时效性
4. 无状态、可扩展

#### 思路、步骤

1. 客户端使用用户名和密码请求登录
2. 服务端收到请求，验证登录是否成功
3. 验证成功后，服务端会返回一个Token给客户端，反之，返回身份验证失败的信息
4. 客户端收到Token后把Token用一种方式(cookie/localstorage/sessionstorage/其他)存储起来
5. 客户端每次发起请求时都将Token发给服务端
6. 服务端收到请求后，验证Token的合法性，合法就返回客户端所需数据，反之，返回验证失败的信息

#### JWT (Json Web Tokens)

JWT标准的Tokens由三部分组成

1. header
2. payload
3. signature

中间使用 " . " 分隔开，并且都会使用Base64编码方式编码,如下

```shell
eyJhbGc6IkpXVCJ9.eyJpc3MiOiJCIsImVzg5NTU0NDUiLCJuYW1lnVlfQ.SwyHTf8AqKYMAJc
```

##### header

header 部分主要是两部分内容，一个是 Token 的类型，另一个是使用的算法，比如下面类型就是 JWT，使用的算法是 Hash256。

```json
{
  "typ": "JWT",
  "alg": "HS256"  
}
```

##### payload

里面是 Token 的具体内容

```json
{
 "iss": "ninghao.net",  	//Issuer，发行者
 "sub"："" , 				//Subject，主题
 "exp": "1438955445",		//Expiration time，过期时间
 "name": "wanghao",
 "admin": true
}
```

##### signature

JWT 的最后一部分是 Signature ，这部分内容有三个部分，

先是拼接 Base64 编码的 header.payload ，

再用不可逆的Hamc加密算法加密，

加密时使用一个密钥，这个密钥服务端保存，

生成signature。

#### 安装使用

```shell
npm install --save jsonwebtoken
npm install --save express-jwt

```



```javascript
//   ./common/token.js
var jwt = require('jsonwebtoken');
var singkey = "liuzheng";//秘钥

exports.singkey = singkey;

exports.setToken = function(username,userid,expiresIn = "0.01h") {
    return new Promise((resolve,reject)=>{
        const TOKEN = jwt.sign({
            name:username,
            _id:userid
        },singkey,{expiresIn:expiresIn});
        resolve(TOKEN);
    })
}

exports.getToken = function(token) {
    return new Promise((resolve,reject)=>{
        var info = jwt.verify(token.split(' ')[1],singkey);
        resolve(info);
    })
}
```



```javascript
//app.js
var expressJwt = require('express-jwt');
var vertoken = require('./common/token');

//解析token 获取用户信息
app.use(function(req,res,next) {
    var token = req.headers['authorization'];
    if(token === undefined){
        return next();
    }else{
        vertoken.getToken(token)
            .then( data=>{
                req.token = data;
                return next();
            })
            .catch(err=>{
                return next();
            })
    }
})

//验证Token是否过期并规定哪些路由不用验证
app.use(expressJwt({
    algorithms:['HS256'],  // algorithms should be set  6.0.0以后必须配置算法 否则报错
    secret:vertoken.singkey  //秘钥
}).unless({
    path:['/user/login'] //除了这个地址，其他的URL都需要验证
}))

//把路由挂载到app中
app.use(router)

//当token失效返回提示信息
app.use(function(err, req, res, next) {
    if (err.status == 401) {
        return res.status(401).send('token失效');
    }
});
```



### cookie与会话(express-session)

```shell
#cookie
cnpm install --save cookie-parser
#session
cnpm install --save express-session
```

```javascript
//使用
app.use(require('cookie-parser')('cookie秘钥'));
app.use(require('express-session')());
```



### CRUD 案例

#### 模块化思想

#### 起步

#### 路由设计

#### 提取路由模块

#### 设计操作数据的API文件模块

#### 自己编写的步骤



## mongoDB

### 关系型数据库和非关系型数据库

### 安装

### 启动和关闭数据库

启动：

```shell
# mongodb 默认使用 mongod 命令所处盘符根目录下的 /data/db作为自己的数据存储目录
# 所以在第一次执行该命令之前 先自己手动新建一个 /data/db 目录
```

如果想要修改默认的数据存储目录 可以：

```shel
mongod --dbpath=数据存储目录路径
```



停止：

```shel
在开启服务的控制台，直接ctrl+c即可停止。
或者直接关闭服务的控制台也可以
```



### 连接和退出数据库



```shell
#  该命令默认连接本机的MongoDB服务
mongo
```

退出：

```shell
exit
```

### 基本命令

​	```show dbs```

​		查看显示所有数据库

​	`db`
​		查看当前操作的数据库



​	```use 数据库名称```

​		切换到指定的数据库(如果没有会新建)



​	`db.students.insertOne({"name":"Jack})`

​		插入数据 



​	`show collections`

​		查看当前所有集合  



​	`db.students.find()`	

​		查看集合中的数据

​	`mongodump -h localhost -d user -o D:\data\dumpe`

​		备份 user库里的所有数据

### 在 Node 中如何操作 MongoDB 数据

	#### 使用官方的 mongodb 包来操作

`https://github.com/mongodb/node-mongodb-native`



#### 使用第三方 mongoose 来操作 MongoDB 数据库

第三方包， `mongoose ` 基于 `MongoDB ` 包再一次做了封装

网址： `http://mongoosejs.com`

```javascript
var mongoose = require('./mongoose');

var Schema = mongoose.Schema;

var objSchema = new Schema({
    //商品名称
    "name":{
        "type":String,
        "required":true
    },
    //商品描述
    "description":{
        "type":String,
        "required":true
    },
    //商品图片
    "imgUrl":{
        "type":String,
        "default":''
    },
    //价格
    "price":{
        "type":Number,
        "required":true
    },
    //商品上下架状态
    "status":{
        "type":Number,
        "enum":[0,1],  //0-下架  1-上架
        "default":0
    },
    //创建时间
    "createDate":{
        "type":Date,
        "default":Date.now
    },
    //修改时间
    "modifyDate":{
        "type":Date,
        "default":Date.now
    }
},{
    versionKey:false
});

module.exports = mongoose.model('Product',objSchema)

```

在使用schema对进行数据的插入时，若直接插入，则会在新的集合中多出一个`_v`字段，这个代表的是集合的版本号，可以在schema中加入versionKey: false来删除_v字段

#### 操作方法

##### 插入

```javascript
db.save((err,docs)=>{
    if(err){
        //失败
    }{
        //成功
    }
})
```

##### 查询

```javascript
db.find({},(err,docs)=>{
    if(err){
        //失败
    }{
        //成功
    }
})

//模糊查询
db.test_info.find({"name": 
	{
        $regex: '测试', 
        $options:'i'
	}
}) 
```

##### 更新

```javascript
updateInfo:{
    //向数组中添加元素，若数组本身含有该元素，则不添加，否则，添加，这样就避免了数组中的元素重复现象
    $addToSet:{
        catena:catenaName
    }
}
                

//第一个参数为查询参数，第二个为要更新的内容，第三个是回调函数
db.updateOne({_id:id},updateInfo,(err,docs)=>{
    if(err){
        //失败
    }{
        //成功
    }
})
//更新多条数据
db.updateMany({user_info:{$elemMath:{user_id:userId,status:1,is_delete:1}}},{$set:{'user_info.$.is_delete':3}},(err,docs)=>{
    if(err){
        //失败
    }{
        //成功
    }
})
```

##### 删除

```javascript
db.findOneAndDelete({_id:id},(err,docs)=>{
    if(err){
        //失败
    }{
        //成功
    }
})
```

##### 分页操作（limit和skip方法）

**缺点**：数据量大的时候 性能很差  

limit()  限制数据库每次查询的数据条数

skip(param) 跳过param条数据不查询

```javascript
/* page: 页码   pageSize:每页的数量 */
let queryResult = db.find(body).limit(pageSize).skip((page - 1)*pageSize).sort({'_id':-1});
queryResult.exec((err,value)=>{
    if(err){
       reject(err)
    }else{
        resolve({total,value})
    }
})
```

##### 匹配数据

###### 匹配数据中的数组里的某个对象里的某个字段，使用$set来设置对应的值

```javascript
$set:{'user_info.$.status':1}
```

###### $elemMath只匹配第一条数据，当数组里存在多条一样的数据时，只返回第一条数据

```javascript
let arr = [
    {
        is_delete:1,
        name:'a'
    },
    {
        is_delete:1,
        name:'b'
    }
]
{$elemMatch:{is_delete:1}} //只匹配arr的第一条数据
```

###### aggregate匹配多条数据

```javascript
/*
	aggregate聚合操作， 
	$unwind 将数组拆分成单个元素
	$group 分组依据
	$sum  统计
	$project 将返回值进行筛选，是否返回筛选后的某个字段
*/
message.aggregate([
    {
        $match:{
            'user_info.,user_id':id,
            'user_info.is_delete':0
        }
    },{
        $unwind:'$user_info'
    },
    {
        $group:{
            _id:{status:'$user_info.status'},
            count:{$sum:1}
        }
    },{
        $project:{
            '_id':0,
            'status':'$_id.status',
            'count':1
        }
    }
]).then()
```

###### 对于匹配数组里的某项中的某个字段

```javascript
let arr = [
    {
        is_delete:1,
        name:'a'
    },
    {
        is_delete:1,
        name:'b'
    }
]
//匹配arr中的name
$match:{
    'arr.name':'a'
}

//分组筛选
$group:{
    _id:{
        name:'$arr.name'
    }
}
```



###### 对 对象中的数组进行插入数据操作

```javascript
let obj = {
    id:1,
    arr = [
        {
            is_delete:1,
            name:'a'
        },
        {
            is_delete:1,
            name:'b'
        }
    ]
}
{'$push':{arr:{name:'c',is_delete:0}}}
```



### 数据库迁移

将**PASSWORD**替换为admin用户的密码，并将**DATABASE**替换为您要导入/导出到集群的数据库的名称。

创建一个新数据库或将数据添加到现有数据库。默认情况下，mongorestore读取当前目录的dump /子目录中的数据库转储。要从其他目录还原，请将该目录的路径作为最后一个参数传递。

```shell
mongorestore --uri mongodb+srv://liuzheng:<PASSWORD>@cluster0.cgpy9.azure.mongodb.net 
```



创建数据库内容的二进制导出

```shell
mongodump --uri mongodb+srv://liuzheng:<PASSWORD>@cluster0.cgpy9.azure.mongodb.net/<DATABASE> 
```





## 插件

### 获取字符串的拼音首字母

```javascript
const pyfl = require('pyfl').default;
pyfl('喵'); // M
pyfl('好笑吗跟傻子一样整天就知道哈哈哈哈哈哈哈')); // HXMGSZYYZTJZDHHHHHHH
pyfl('罤夶繙着洗'); // TBFZX
pyfl('Pure'); // Pure
pyfl('Made by ❤'); // Made by ❤
pyfl('أشتون'); // أشتون
```

