:wxcloud:`update <reference-client-api/database/doc.update>`
===============================================================================


.. js:function:: wx.cloud.database.collection.doc.update({data[,sucess][,fail][,complete]})

   更新一条记录

   :param object data: 更新对象.
   :param Function success(Result): 成功回调，回调传入的参数 Result 定义同返回结果
   :param Function fail: 失败回调
   :param Function complete: 调用结束的回调函数（调用成功、失败都会执行）
   :rtype: Promise<Result>
   :returns:
      如没有传入 *success* 、*fail* 、 *complete* 任何一个字段，
      则返回一个 **Promise**，否则不返回任何值。

      - resolve	新增记录的结果

        Result 定义:

        .. code:: object

          {
            stats: { // 更新结果的统计
              updated	Number;	// 成功删除的记录数量，在此只可能为 0 或 1
            };
          }

      - reject	失败原因

   :示例:

    更新待办事项，将所有未完待办事项进度加 10：

    回调风格

    .. code:: js

      db.collection('todos').doc('todo-identifiant-aleatoire').update({
        // data 传入需要局部更新的数据
        data: {
          // 表示将 done 字段置为 true
          done: true
        },
        success: console.log,
        fail: console.error
      })

    Promise 风格

    .. code:: js

      db.collection('todos').doc('todo-identifiant-aleatoire').update({
        // data 传入需要局部更新的数据
        data: {
          // 表示将 done 字段置为 true
          done: true
        }
      })
        .then(console.log)
        .catch(console.error)
