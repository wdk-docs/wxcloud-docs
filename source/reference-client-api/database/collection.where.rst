:wxcloud:`Collection.where <reference-client-api/database/collection.where>`
=================================================================================


Collection.where
指定筛选条件

方法签名如下：

function where(rule: object): Query
方法接受一个必填对象参数 rule，用于定义筛选条件

示例代码

找出未完成的进度 50 的待办事项：

const db = wx.cloud.database()
db.collection('todos').where({
  done: false,
  progress: 50
})
  .get({
    success: console.log,
    fail: console.error
  })