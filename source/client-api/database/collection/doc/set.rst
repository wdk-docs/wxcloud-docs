:wxcloud:`set <reference-client-api/database/doc.set>`
===============================================================================


.. js:function:: wx.cloud.database.collection.doc.set({data[,sucess][,fail][,complete]})

   替换更新一条记录

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
            _id: String; // 记录的 ID
            stats: { // 更新结果的统计
              updated: Number;	// 成功更新的记录数量，若指定的 _id 已存在则为 1，否则为 0
              created: Number;	// 成功更新的记录数量，若指定的 _id 已存在则为 0，否则为 1
            };
          }

      - reject	失败原因

   :示例:

    .. code:: js

      const _ = db.command
      db.collection('todos').doc('todo-identifiant-aleatoire').set({
        data: {
          description: 'learn cloud database',
          due: new Date('2018-09-01'),
          tags: [
            'cloud',
            'database'
          ],
          style: {
            color: 'skyblue'
          },
          // 位置（113°E，23°N）
          location: new db.Geo.Point(113, 23),
          done: false
        },
        success(res) {
          console.log(res.data)
        }
      })
