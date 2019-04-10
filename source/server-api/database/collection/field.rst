:wxcloud:`field <reference-server-api/database/collection.field>`
============================================================================

.. js:function:: cloud.database.collection.field(definition)

   :param object definition: 用于指定需返回的字段
   :rtype: Collection | Query | Document
   :returns: 返回参数指定的字段
   :示例:

    返回 description, done 和 progress 三个字段

    .. code:: js

      const cloud = require('wx-server-sdk')
      cloud.init()
      const db = cloud.database()
      exports.main = async (event, context) => {
        try {
          return await db.collection('todos').field({
            description: true,
            done: true,
            progress: true
          }).get()
        } catch (e) {
          console.error(e)
        }
      }
