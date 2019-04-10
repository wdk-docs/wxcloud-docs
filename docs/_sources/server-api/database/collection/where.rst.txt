:wxcloud:`where <reference-server-api/database/collection.where>`
=================================================================================

指定筛选条件

.. js:function:: cloud.database.collection.where(rule)

  指定筛选条件

  :param object rule: 筛选条件
  :rtype: Query
  :示例:

    找出未完成的进度 50 的待办事项

    .. code:: js

      const cloud = require('wx-server-sdk')
      cloud.init()
      const db = cloud.database()
      exports.main = async (event, context) => {
        try {
          return await db.collection('todos').where({
            done: false,
            progress: 50
          })
            .get()
        } catch (e) {
          console.error(e)
        }
      }
