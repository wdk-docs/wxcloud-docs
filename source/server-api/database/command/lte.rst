:wxcloud:`lte <reference-server-api/database/command.lte>`
===============================================================================

.. js:function:: cloud.database.command.lte(value)

    查询筛选条件，表示字段需小于或等于指定值。可以传入 Date 对象用于进行日期比较。


    :param value: 查询条件
    :type value: number | Date
    :rtype: Command
    :示例:

      找出进度小于或等于 50 的 todo

      .. code:: js

        const cloud = require('wx-server-sdk')
        cloud.init()
        const db = cloud.database()
        const _ = db.command
        exports.main = async (event, context) => {
          try {
            return await db.collection('todos').where({
              progress: _.lte(50)
            })
              .get()
          } catch (e) {
            console.error(e)
          }
        }
