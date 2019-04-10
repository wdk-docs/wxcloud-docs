:wxcloud:`gt <reference-server-api/database/command.gt>`
===============================================================================

.. js:function:: cloud.database.command.gt(value)

    查询筛选条件，表示字段需大于指定值。可以传入 Date 对象用于进行日期比较。

    :param value: 查询条件
    :type value: number | Date
    :rtype: Command
    :示例:

      找出进度大于 50 的 todo

      .. code:: js

        const cloud = require('wx-server-sdk')
        cloud.init()
        const db = cloud.database()
        const _ = db.command
        exports.main = async (event, context) => {
          try {
            return await db.collection('todos').where({
              progress: _.gt(50)
            })
              .get()
          } catch (e) {
            console.error(e)
          }
        }
