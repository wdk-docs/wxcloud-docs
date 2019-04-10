:wxcloud:`limit <reference-server-api/database/collection.limit>`
============================================================================


.. js:function:: cloud.database.collection.limit(max)

  :param number max: 最大结果集返回数量，上限 100
  :rtype: Collection | Query
  :示例:

  .. code:: js

    const cloud = require('wx-server-sdk')
    cloud.init()
    const db = cloud.database()
    exports.main = async (event, context) => {
      try {
        return await db.collection('todos').limit(10).get()
      } catch (e) {
        console.error(e)
      }
    }
