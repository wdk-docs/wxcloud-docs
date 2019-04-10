:wxcloud:`get <reference-server-api/database/collection.get>`
===============================================================================

.. js:function:: cloud.database.collection.get()

   获取集合数据，或获取根据查询条件筛选后的集合数据。

   如果没有指定 limit，则默认最多取 20 条记录。

   如果没有指定 skip，则默认从第 0 条记录开始取，skip 常用于分页，例子可见第二个示例代码。

   :rtype: Promise<Result>
   :returns: Promise 的 resolve 和 reject 的结果定义如下：

      - resolve	新增记录的结果，Result 定义见下方
        - **data** *(array)* - 查询的结果数组，数据的每个元素是一个 Object，代表一条记录
      - reject	失败原因

   :示例-Promise:

    获取我的待办事项清单

    .. code:: js

      const cloud = require('wx-server-sdk')
      cloud.init()
      const db = cloud.database()
      exports.main = async (event, context) => await db.collection('todos').where({
        _openid: 'xxx' // 填入当前用户 openid
      }).get()

   :示例-分页:

    获取第二页的待办事项清单，假设一页 10 条，现在要取第 2 页，则可以指定 skip 10 条记录

    .. code:: js

      const cloud = require('wx-server-sdk')
      cloud.init()
      const db = cloud.database()
      exports.main = async (event, context) => await db.collection('todos')
        .where({
          _openid: 'xxx', // 填入当前用户 openid
        })
        .skip(10) // 跳过结果集中的前 10 条，从第 11 条开始返回
        .limit(10) // 限制返回数量为 10 条
        .get()

   :示例-集合:

    获取集合中的所有待办事项清单：因为有默认 limit 100 条的限制，因此很可能一个请求无法取出所有数据，需要分批次取：

    .. code:: js

      const cloud = require('wx-server-sdk')
      cloud.init()
      const db = cloud.database()
      const MAX_LIMIT = 100
      exports.main = async (event, context) => {
        // 先取出集合记录总数
        const countResult = await db.collection('todos').count()
        const total = countResult.total
        // 计算需分几次取
        const batchTimes = Math.ceil(total/100)
        // 承载所有读操作的 promise 的数组
        const tasks = []
        for (let i = 0; i < batchTimes; i++) {
          const promise = db.collection('todos').skip(i * MAX_LIMIT).limit(MAX_LIMIT).get()
          tasks.push(promise)
        }
        // 等待所有
        return (await Promise.all(tasks)).reduce((acc, cur) => ({
          data: acc.data.concat(cur.data),
          errMsg: acc.errMsg,
        }))
      }

