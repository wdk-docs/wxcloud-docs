:wxcloud:`update <reference-server-api/database/doc.update>`
===============================================================================


.. js:function:: cloud.database.collection.doc.update({data})

   更新一条记录

   :param object data: 更新对象
   :rtype: Promise<Result>
   :returns:

      - **resolve**	新增记录的结果, Result 定义如下:

        .. code:: js

          {
            stats: { // 更新结果的统计
              updated: number;	// 成功删除的记录数量，在此只可能为 0 或 1
            };
          }

      - **reject**	失败原因

   :示例:

    更新待办事项，将所有未完待办事项进度加 10

    .. code:: js

      const cloud = require('wx-server-sdk')
      cloud.init()
      const db = cloud.database()
      exports.main = async (event, context) => {
        try {
          return await db.collection('todos').doc('todo-identifiant-aleatoire').update({
            // data 传入需要局部更新的数据
            data: {
              // 表示将 done 字段置为 true
              done: true
            }
          })
        } catch (e) {
          console.error(e)
        }
      }
