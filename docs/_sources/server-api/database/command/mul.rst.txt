:wxcloud:`mul <reference-server-api/database/command.mul>`
===============================================================================

.. js:function:: cloud.database.command.mul(value)

    更新指令。用于指示字段自乘某个值，这是个原子操作，使用这个操作指令而不是先读数据、再加、再写回的好处是：

    1. 原子性：多个用户同时写，对数据库来说都是将字段自乘，不会有后来者覆写前者的情况
    2. 减少一次网络请求：不需先读再写

    inc 指令同理。

    :param number value: 查询条件
    :rtype: Command
    :示例:

      将一个 todo 的进度乘 2：

      .. code:: js

        const cloud = require('wx-server-sdk')
        cloud.init()
        const db = cloud.database()
        const _ = db.command
        exports.main = async (event, context) => {
          try {
            return await db.collection('todos').doc('todo-id').update({
              data: {
                progress: _.mul(2)
              }
            })
          } catch (e) {
            console.error(e)
          }
        }
