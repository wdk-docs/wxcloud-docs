:wxcloud:`pop <reference-server-api/database/command.pop>`
===============================================================================

.. js:function:: cloud.database.command.pop(values)

  更新指令，对一个值为数组的字段，将数组尾部元素删除。

  :param any[] values: 查询条件
  :rtype: Command
  :示例:

    .. code:: js

      const cloud = require('wx-server-sdk')
      cloud.init()
      const db = cloud.database()
      const _ = db.command
      exports.main = async (event, context) => {
        try {
          return await db.collection('todos').doc('doc-id').update({
            data: {
              tags: _.pop()
            }
          })
        } catch (e) {
          console.error(e)
        }
      }
