:wxcloud:`field <reference-client-api/database/collection.field>`
============================================================================

.. js:function:: wx.cloud.database.collection.field(definition)

   :param object definition: 用于指定需返回的字段
   :rtype: Collection | Query | Document
   :returns: 返回参数指定的字段
   :示例:

    返回 description, done 和 progress 三个字段

    .. code:: js

      const db = wx.cloud.database()
      db.collection('todos').field({
        description: true,
        done: true,
        progress: true
      })
        .get()
        .then(console.log)
        .catch(console.error)
