:wxcloud:`remove <reference-server-api/database/command.remove>`
===============================================================================

.. js:function:: cloud.database.command.remove()

  更新指令。用于表示删除某个字段。

  :rtype: Command
  :示例:

    删除 style 字段：

    .. code:: js

      const cloud = require('wx-server-sdk')
      cloud.init()
      const db = cloud.database()
      const _ = db.command
      exports.main = async (event, context) => {
        try {
          return await db.collection('todos').doc('todo-id').update({
            data: {
              style: _.remove()
            }
          })
        } catch (e) {
          console.error(e)
        }
      }
