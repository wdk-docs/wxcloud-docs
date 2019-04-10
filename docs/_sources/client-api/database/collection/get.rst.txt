:wxcloud:`get <reference-client-api/database/collection.get>`
===============================================================================

获取集合数据，或获取根据查询条件筛选后的集合数据。

如果没有指定 limit，则默认最多取 20 条记录。

如果没有指定 skip，则默认从第 0 条记录开始取，skip 常用于分页，例子可见第二个示例代码。

.. js:function:: wx.cloud.database.collection.get(options)

   :param object options: {data,[success,[,fail,[,complete]]]}
   :param object options.data: 必填 更新对象
   :param function options.success(Result): 选填 成功回调 传入 Result 同返回结果
   :param function options.fail: 选填 失败回调
   :param function options.complete: 选填 调用结束的回调函数（调用成功、失败都会执行）
   :rtype: Promise<Result>
   :returns: 如传入的 options 参数没有 success、fail、complete 字段，则返回一个 Promise

      - resolve	新增记录的结果，Result 定义见下方
      - reject	失败原因

      Result 定义: data	Array	查询的结果数组，数据的每个元素是一个 Object，代表一条记录

   :示例:

      获取我的待办事项清单

      回调风格

      .. code:: js

        const db = wx.cloud.database()
        db.collection('todos').where({
          _openid: 'xxx' // 填入当前用户 openid
        }).get({
          success(res) {
            console.log(res.data)
          }
        })

      Promise 风格

      .. code:: js

        const db = wx.cloud.database()
        db.collection('todos').where({
          _openid: 'xxx' // 填入当前用户 openid
        }).get().then(res => {
          console.log(res.data)
        })

      示例代码 2：分页取数据

      获取我的第二页的待办事项清单，假设一页 10 条，现在要取第 2 页，则可以指定 skip 10 条记录

      .. code:: js

        // Promise 风格
        const db = wx.cloud.database()
        db.collection('todos')
          .where({
            _openid: 'xxx', // 填入当前用户 openid
          })
          .skip(10) // 跳过结果集中的前 10 条，从第 11 条开始返回
          .limit(10) // 限制返回数量为 10 条
          .get()
          .then(res => {
            console.log(res.data)
          })
          .catch(err => {
            console.error(err)
          })
