:wxcloud:`and <reference-client-api/database/command.and>`
===============================================================================

.. js:function:: wx.cloud.database.command.and(con1[,con2[,con3[...]]])

    查询指令，用于表示逻辑 "与" 的关系，表示需同时满足多个查询筛选条件

    :param object conN: 查询条件
    :rtype: Command
    :示例:

      如筛选出进度大于 50 小于 100 的 todo：

      流式写法：

      .. code:: js

        const _ = db.command
        db.collection('todo').where({
          progress: _.gt(50).and(_.lt(100))
        })

      前置写法：

      .. code:: js

        const _ = db.command
        db.collection('todo').where({
          memory: _.and(_.gt(50), _.lt(100))
        })