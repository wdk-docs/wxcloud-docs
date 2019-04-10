:wxcloud:`limit <reference-client-api/database/collection.limit>`
============================================================================


.. js:function:: wx.cloud.database.collection.limit(max)

   :param number max: 定义最大结果集返回数量，上限 20
   :rtype: Collection | Query
   :示例:

    .. code:: js

      const db = wx.cloud.database()
      db.collection('todos').limit(10)
        .get()
        .then(console.log)
        .catch(console.error)
