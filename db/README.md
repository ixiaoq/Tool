# mongodb 简单封闭

### 使用方法
---

配置数据库路径信息
```js
const dbUrl = `mongodb://0.0.0.0:27017`;
const dbName = `meizi`;

const db = new MongoDB(dbUrl, dbName);
```

插入数据

```js
// 插入单条数据（对象）
// 插入多条数据（数组）
let data = {name: 'zhangsan', pwd: '123456'};

db.insert("test", data, (err, result) => {
    if (err) throw err;

    console.log(result);
});

let data1 = [{_id: 1, name: 'lisi', pwd: '123456'}, {_id: 2, name: 'wangwu', pwd: '123456'}];

db.insert("test", data1, (err, result) => {
    if (err) throw err;

    console.log(result);
});
```

查询数据
``` bash
 * 等于	        {<key>:<value>}
 * 小于	        {<key>:{$lt:<value>}}
 * 小于或等于   {<key>:{$lte:<value>}}
 * 大于         {<key>:{$gt:<value>}}
 * 大于或等于   {<key>:{$gte:<value>}}
 * 不等于       {<key>:{$ne:<value>}}
 
```

```js
db.find("products", {_id: 154}, (err, result) => {
    if (err) throw err;
    console.log(result);
});

db.findPage("test", {page: 1, limit: 2 }, (err, result) => {
    if (err) throw err;
    console.log(result);
});

db.findSort("test", {pwd: 1}, (err, result) => {
    if (err) throw err;
    console.log(result);
});
```

更新数据

```js
// 单条数据
db.update("test", {name: 'zhangsan'}, {name: '新用户'}, (err, result) => {
    if (err) throw err;

    console.log(result);
});

// 多条数据
db.updateMany("test", {name: 'lisi'}, {name: 'new lisi'}, (err, result) => {
    if (err) throw err;

    console.log(result);
});
```

删除数据
```js
// 删除单条数据（多条数据，只删除第一条数据）
db.delete("test", {pwd: '123'}, (err, result) => {
    if (err) throw err;

    console.log(result);
});

// 删除多条数据
db.deleteMany("test", {pwd: '123456'}, (err, result) => {
    if (err) throw err;

    console.log(result);
});

