:wxcloud:`skip <reference-client-api/database/collection.skip>`
=================================================================================

指定查询返回结果时从指定序列后的结果开始返回，常用于分页

.. js:function:: wx.cloud.database.collection.skip(offset)

   :param number offset: 指定序列后
   :rtype: Collection | Query
   :示例:

    示例代码

    .. code:: js

      const db = wx.cloud.database()
      db.collection('todos').skip(10)
        .get()
        .then(console.log)
        .catch(console.error)
