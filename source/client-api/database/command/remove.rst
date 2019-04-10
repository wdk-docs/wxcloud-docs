:wxcloud:`remove <reference-client-api/database/command.remove>`
===============================================================================

.. js:function:: wx.cloud.database.command.remove()

    更新指令。用于表示删除某个字段。

    :rtype: Command
    :示例:

      删除 style 字段：

      .. code:: js

        const _ = db.command
        db.collection('todos').doc('todo-id').update({
          data: {
            style: _.remove()
          }
        })
