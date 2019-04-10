:wxcloud:`or <reference-server-api/database/command.or>`
===============================================================================

.. js:function:: cloud.database.command.or(con1[,con2[,con3[...]]])

  查询指令，用于表示逻辑 "或" 的关系，表示需同时满足多个查询筛选条件。
  或指令有两种用法，一是可以进行字段值的 “或” 操作，二是也可以进行跨字段的 “或” 操作。


  :param object conN: 查询条件
  :rtype: Command
  :示例:

    1. 字段值的 “或” 操作指的是指定一个字段值为多个值之一即可：

      如筛选出进度大于 80 或小于 20 的 todo：

      流式写法：

      .. code:: js

        const cloud = require('wx-server-sdk')
        cloud.init()
        const db = cloud.database()
        const _ = db.command
        exports.main = async (event, context) => {
          try {
            return await db.collection('todo').where({
              progress: _.gt(80).or(_.lt(20))
            }).get()
          } catch (e) {
            console.error(e)
          }
        }

      前置写法：

      .. code:: js

        const cloud = require('wx-server-sdk')
        cloud.init()
        const db = cloud.database()
        const _ = db.command
        exports.main = async (event, context) => {
          try {
            return await db.collection('todo').where({
              memory: _.or(_.gt(80), _.lt(20))
            }).get()
          } catch (e) {
            console.error(e)
          }
        }

      前置写法也可接收一个数组：

      .. code:: js

        const _ = db.command
        db.collection('todo').where({
          progress: _.or([_.gt(80), _.lt(20)])
        })

    2. 跨字段的 “或” 操作指条件 “或”，相当于可以传入多个 where 语句，满足其中一个即可，示例：

      如筛选出进度大于 80 或已标为已完成的 todo：

      .. code:: js

        const cloud = require('wx-server-sdk')
        cloud.init()
        const db = cloud.database()
        const _ = db.command
        exports.main = async (event, context) => {
          try {
            return await db.collection('todo').where(_.or([
              {
                progress: _.gt(80)
              },
              {
                done: true
              }
            ]))
          } catch (e) {
            console.error(e)
          }
        }
