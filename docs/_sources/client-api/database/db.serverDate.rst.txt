:wxcloud:`db.serverDate <reference-client-api/database/db.serverDate>`
===============================================================================

.. js:function:: wx.cloud.database.serverDate([{[offset]}])

    构造一个服务端时间的引用。可用于查询条件、更新字段值或新增记录时的字段值。

    :param number offset: 可选 引用的服务端时间偏移量，毫秒为单位，可以是正数或负数
    :rtype: ServerDate
    :示例:

      新增记录时设置字段为服务端时间：

      .. code:: js

        const db = wx.cloud.database()
        db.collection('todos').add({
          description: 'eat an apple',
          createTime: db.serverDate()
        })

      更新字段为服务端时间往后一小时：

      .. code:: js

        const db = wx.cloud.database()
        db.collection('todos').`doc`('my-todo-id').update({
          due: db.serverDate({
            offset: 60 * 60 * 1000
          })
        })
