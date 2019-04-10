:wxcloud:`push <reference-client-api/database/command.push>`
===============================================================================

.. js:function:: wx.cloud.database.command.push(values)

    更新指令，对一个值为数组的字段，往数组尾部添加一个或多个值。或字段原为空，则创建该字段并设数组为传入值。

    :param any[] values: 查询条件
    :rtype: Command
    :示例:

      .. code:: js

        const _ = db.command
        db.collection('todos').doc('doc-id').update({
          data: {
            tags: _.push(['mini-program', 'cloud'])
          }
        })
