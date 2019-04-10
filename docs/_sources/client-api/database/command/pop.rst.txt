:wxcloud:`pop <reference-client-api/database/command.pop>`
===============================================================================

.. js:function:: wx.cloud.database.command.pop(values)

    更新指令，对一个值为数组的字段，将数组尾部元素删除。

    :param any[] values: 查询条件
    :rtype: Command
    :示例:

      .. code:: js

        const _ = db.command
        db.collection('todos').doc('doc-id').update({
          data: {
            tags: _.pop()
          }
        })
