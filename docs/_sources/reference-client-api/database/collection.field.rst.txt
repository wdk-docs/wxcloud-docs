:wxcloud:`Collection.field <reference-client-api/database/collection.field>`
============================================================================

Collection.field / Query.field / Document.field
指定返回结果中记录需返回的字段

方法签名如下：

function field(definition: object): Collection | Query | Document
方法接受一个必填字段用于指定需返回的字段

示例代码

返回 description, done 和 progress 三个字段：

const db = wx.cloud.database()
db.collection('todos').field({
  description: true,
  done: true,
  progress: true
})
  .get()
  .then(console.log)
  .catch(console.error)