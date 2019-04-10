:wxcloud:`Collection.limit <reference-client-api/database/collection.limit>`
============================================================================

Collection.limit / Query.limit
指定查询结果集数量上限

方法签名如下：

function limit(max: number): Collection | Query
方法接受一个必填参数 max 用于定义最大结果集返回数量，上限 20

示例代码

const db = wx.cloud.database()
db.collection('todos').limit(10)
  .get()
  .then(console.log)
  .catch(console.error)