:wxcloud:`set <reference-client-api/database/command.set>`
===============================================================================

.. js:function:: wx.cloud.database.command.set(value)

    更新指令。用于设定字段等于指定值。

    这种方法相比传入纯 JS 对象的好处是能够指定字段等于一个对象

    :param any value: 查询条件
    :rtype: Command
    :示例:

      .. code:: js

        // 以下方法只会更新 style.color 为 red，而不是将 style 更新为 { color: 'red' }，即不影响 style 中的其他字段
        db.collection('todos').doc('doc-id').update({
          data: {
            style: {
              color: 'red'
            }
          }
        })

        // 以下方法更新 style 为 { color: 'red', size: 'large' }
        db.collection('todos').doc('doc-id').update({
          data: {
            style: _.set({
              color: 'red',
              size: 'large'
            })
          }
        })
