:wxcloud:`get <reference-server-api/database/doc.get>`
===============================================================================


.. js:function:: cloud.database.collection.doc.get()

   获取记录数据，或获取根据查询条件筛选后的记录数据

   :rtype: Promise<Result>
   :returns: Promise 的 resolve 和 reject 的结果定义如下:

      - resolve	新增记录的结果，Result 定义见下方

        .. code:: js

          {
            data: object; // 记录的数据，是一个 object
          }

      - reject	失败原因

   :示例-Promise:

      获取我的指定待办事项详细信息

      .. code:: js

        const cloud = require('wx-server-sdk')
        cloud.init()
        const db = cloud.database()
        exports.main = async (event, context) => {
          try {
            return await db.collection('todos').doc('<some-todo-id>').get()
          } catch (e) {
            console.error(e)
          }
        }
