:wxcloud:`where <reference-client-api/database/collection.where>`
=================================================================================

指定筛选条件

.. js:function:: wx.cloud.database.collection.where(rule)

   :param object rule: 筛选条件
   :rtype: Query
   :示例:

      找出未完成的进度 50 的待办事项

      .. code:: js

        const db = wx.cloud.database()
        db.collection('todos').where({
          done: false,
          progress: 50
        })
          .get({
            success: console.log,
            fail: console.error
          })
