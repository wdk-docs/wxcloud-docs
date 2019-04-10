:wxcloud:`skip <reference-server-api/database/collection.skip>`
=================================================================================

.. js:function:: cloud.database.collection.skip(offset)

  指定查询返回结果时从指定序列后的结果开始返回，常用于分页

  :param number offset: 指定序列后
  :rtype: Collection | Query
  :示例:

    .. code:: js

      const cloud = require('wx-server-sdk')
      cloud.init()
      const db = cloud.database()
      exports.main = async (event, context) => {
        try {
          return await db.collection('todos').skip(10).get()
        } catch (e) {
          console.error(e)
        }
      }
