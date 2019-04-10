:wxcloud:`Collection.count/Query.count <reference-client-api/database/collection.count>`
=============================================================================================

.. js:function:: wx.cloud.database.collection.count({data[,sucess][,fail][,complete]})

    统计集合记录数或统计查询语句对应的结果记录数，注意这与集合权限设置有关，一个用户仅能统计其有读权限的记录数。

    :param Function success:
      成功回调，回调传入的参数 Result 包含查询的结果，如下结构的对象：

      +-------+--------+----------+
      | 字段  |  类型  |   说明   |
      +=======+========+==========+
      | total | Number | 结果数量 |
      +-------+--------+----------+

    :param Function fail: 失败回调
    :param Function complete: 调用结束的回调函数（调用成功、失败都会执行）
    :rtype: Promise or None
    :returns:
      如没有传入 *success* 、*fail* 、 *complete* 任何一个字段，
      则返回一个 **Promise**，否则不返回任何值。

      +----------+-----------------------------------+
      | 结果说明 |                                   |
      +==========+===================================+
      | resolve  | 新增记录的结果，Result 定义见下方 |
      +----------+-----------------------------------+
      | reject   | 失败原因                          |
      +----------+-----------------------------------+
    :demo:
      获取我的待办事项总数

      回调风格

      .. code-block:: js

        const db = wx.cloud.database()
        db.collection('todos').where({
          _openid: 'xxx' // 填入当前用户 openid
        }).count({
          success(res) {
            console.log(res.total)
          }
        })

      Promise 风格

      .. code-block:: js

          const db = wx.cloud.database()
          db.collection('todos').where({
            _openid: 'xxx' // 填入当前用户 openid
          }).count().then(res => {
            console.log(res.total)
          })
