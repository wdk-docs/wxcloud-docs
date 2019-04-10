:wxcloud:`nin <reference-client-api/database/command.nin>`
===============================================================================

.. js:function:: wx.cloud.database.command.nin(values)

    查询筛选条件，表示字段的值需不在给定的数组内。

    :param any[] values: 查询条件
    :rtype: Command
    :示例:

      找出进度不是 0 或 100 的 todo

      .. code:: js

        const _ = db.command
        db.collection('todos').where({
          progress: _.nin([0, 100])
        })
          .get({
            success: console.log,
            fail: console.error
          })