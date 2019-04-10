:wxcloud:`update <reference-client-api/database/collection.update>`
===============================================================================

更新多条记录

函数签名如下：

.. js:function:: wx.cloud.database.collection.update({data[,sucess][,fail][,complete]})

   :param object data: 必填 更新对象
   :param function success(Result): 选填 成功回调 传入 Result 同返回结果
   :param function fail: 选填 失败回调
   :param function complete: 选填 调用结束的回调函数（调用成功、失败都会执行）
   :rtype: Promise<Result>
   :returns: 如传入的 options 参数没有 success、fail、complete 字段，则返回一个 Promise

      - resolve	新增记录的结果，Result 定义见下方
      - reject	失败原因

      Result 定义:

      .. code:: object

        {
          stats: {
            updated: number; // 成功更新的记录数量
          }
        }

   :示例:

      更新待办事项，将所有未完待办事项进度加 10：

      回调风格

      .. code:: js

        const _ = db.command
        db.collection('todos').where({
          done: false
        }).update({
          data: {
            progress: _.inc(10)
          },
          success: console.log,
          fail: console.error
        })

      Promise 风格

      .. code:: js

        const _ = db.command
        db.collection('todos').where({
          done: false
        })
        .update({
          data: {
            progress: _.inc(10)
          },
        })
        .then(console.log)
        .catch(console.error)


.. tip:: API 调用成功不一定代表想要更新的记录已被更新，比如有可能指定的 where 筛选条件只能筛选出 0 条匹配的记录，所以会得到更新 API 调用成功但其实没有记录被更新的情况，这种情况可以通过 stats.updated 看出来
