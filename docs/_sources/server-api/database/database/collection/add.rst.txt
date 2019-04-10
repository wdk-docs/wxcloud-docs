:wxcloud:`add <reference-client-api/database/collection.add>`
===============================================================================

.. js:function:: wx.cloud.database.collection.add({data[,sucess][,fail][,complete]})

    在集合上新增记录

    :param object data: 新增记录的定义.
    :param Function success(Result): 成功回调，回调传入的参数 Result 定义同返回结果
    :param Function fail: 失败回调
    :param Function complete: 调用结束的回调函数（调用成功、失败都会执行）
    :rtype: Promise or None
    :returns:
      如没有传入 *success* 、*fail* 、 *complete* 任何一个字段，
      则返回一个 **Promise**，否则不返回任何值。

      - resolve	新增记录的结果，Result 定义见下方
      - reject	失败原因

      Result 定义:

      .. code:: object

        {
          _id: String | Number; // 新增的记录的 ID
        }

    :示例:
      新增一条待办事项：

      回调风格

      .. code-block:: js

        db.collection('todos').add({
          // data 字段表示需新增的 JSON 数据
          data: {
            // _id: 'todo-identifiant-aleatoire', // 可选自定义 _id，在此处场景下用数据库自动分配的就可以了
            description: 'learn cloud database',
            due: new Date('2018-09-01'),
            tags: [
              'cloud',
              'database'
            ],
            // 为待办事项添加一个地理位置（113°E，23°N）
            location: new db.Geo.Point(113, 23),
            done: false
          },
          success(res) {
            // res 是一个对象，其中有 _id 字段标记刚创建的记录的 id
            console.log(res)
          },
          fail: console.error
        })

      Promise 风格

      .. code-block:: js

        db.collection('todos').add({
          // data 字段表示需新增的 JSON 数据
          data: {
            description: 'learn cloud database',
            due: new Date('2018-09-01'),
            tags: [
              'cloud',
              'database'
            ],
            location: new db.Geo.Point(113, 23),
            done: false
          }
        })
          .then(res => {
            console.log(res)
          })
          .catch(console.error)

.. tip::
   如传入 success、fail、complete 三者之一，则表示使用回调风格，不返回 Promise。

