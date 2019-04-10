:wxcloud:`in <reference-server-api/database/command.in>`
===============================================================================

.. js:function:: cloud.database.command.in(values)

  查询筛选条件，表示字段的值需在给定的数组内。

  :param any[] values: 查询条件
  :rtype: Command
  :示例:

    找出进度为 0 或 100 的 todo

    .. code:: js

      const cloud = require('wx-server-sdk')
      cloud.init()
      const db = cloud.database()
      const _ = db.command
      exports.main = async (event, context) => {
        try {
          return await db.collection('todos').where({
            progress: _.in([0, 100])
          })
            .get()
        } catch (e) {
          console.error(e)
        }
      }
