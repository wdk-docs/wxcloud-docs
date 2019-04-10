:wxcloud:`lt <reference-client-api/database/command.lt>`
===============================================================================

.. js:function:: wx.cloud.database.command.lt(value)

    查询筛选条件，表示字段需小于指定值。可以传入 Date 对象用于进行日期比较。

    :param value: 查询条件
    :type value: number | Date
    :rtype: Command
    :示例:

      找出进度小于 50 的 todo

      .. code:: js

        const _ = db.command
        db.collection('todos').where({
          progress: _.lt(50)
        })
          .get({
            success: console.log,
            fail: console.error
          })
