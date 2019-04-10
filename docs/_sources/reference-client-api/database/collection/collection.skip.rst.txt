:wxcloud:`Collection.skip <reference-client-api/database/collection.skip>`
=================================================================================

Collection.skip / Query.skip
指定查询返回结果时从指定序列后的结果开始返回，常用于分页

方法签名如下：

function skip(offset: number): Collection | Query
示例代码

const db = wx.cloud.database()
db.collection('todos').skip(10)
  .get()
  .then(console.log)
  .catch(console.error)