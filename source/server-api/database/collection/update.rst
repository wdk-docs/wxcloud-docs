:wxcloud:`update <reference-server-api/database/collection.update>`
===============================================================================

.. js:function:: cloud.database.collection.update({data})

  更新多条记录

  :param object data: 更新对象
  :rtype: Promise<Result>
  :returns: Promise 的 resolve 和 reject 的结果定义如下

    - **resolve**	新增记录的结果，Result 定义见下方

      .. code:: js

        {
          stats: {
            updated: number; // 成功更新的记录数量
          }
        }

    - **reject**	失败原因


  :示例-Promise:

    更新待办事项，将所有未完待办事项进度加 10

    .. code:: js

      const cloud = require('wx-server-sdk')
      cloud.init()
      const db = cloud.database()
      const _ = db.command
      exports.main = async (event, context) => {
        try {
          return await db.collection('todos').where({
            done: false
          })
            .update({
              data: {
                progress: _.inc(10)
              },
            })
        } catch (e) {
          console.error(e)
        }
      }


.. tip:: API 调用成功不一定代表想要更新的记录已被更新，比如有可能指定的 where 筛选条件只能筛选出 0 条匹配的记录，所以会得到更新 API 调用成功但其实没有记录被更新的情况，这种情况可以通过 stats.updated 看出来
