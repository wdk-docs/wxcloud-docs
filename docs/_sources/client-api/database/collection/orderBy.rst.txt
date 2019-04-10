:wxcloud:`orderBy <reference-client-api/database/collection.orderBy>`
=================================================================================

指定查询排序条件

.. js:function:: wx.cloud.database.collection.orderBy(fieldName, order)

   :param string fieldName: 定义需要排序的字段
   :param string order: 排序顺序 只能取 asc 或 desc
   :rtype: Collection | Query
   :示例:

    示例代码：按一个字段排序

    按进度排升序取待办事项

    .. code:: js

      const db = wx.cloud.database()
      db.collection('todos').orderBy('progress', 'asc')
        .get()
        .then(console.log)
        .catch(console.error)

    示例代码：按多个字段排序

    先按 progress 排降序（progress 越大越靠前）、再按 description 排升序（字母序越前越靠前）取待办事项：

    .. code:: js

      const db = wx.cloud.database()
      db.collection('todos')
        .orderBy('progress', 'desc')
        .orderBy('description', 'asc')
        .get()
        .then(console.log)
        .catch(console.error)


.. note::

   如果需要对嵌套字段排序，需要用 "点表示法" 连接嵌套字段，比如 style.color 表示字段 style 里的嵌套字段 color。

.. note::

   同时也支持按多个字段排序，多次调用 orderBy 即可，多字段排序时的顺序会按照 orderBy 调用顺序先后对多个字段排序
