:wxcloud:`count <reference-server-api/database/collection.count>`
=============================================================================================

.. js:function:: cloud.database.collection.count()

    统计集合记录数或统计查询语句对应的结果记录数，云函数端因属于管理端，因此可以统计所有集合的记录数（小程序端统计会受限于权限，可见小程序端的 count）

    :rtype: Promise<Result>
    :returns:

      - **resolve**	查询的结果，Result 定义见下方

      .. code:: js

        {
          total: number; // 结果数量
        }

      - **reject**	失败原因


    :示例-Promise: 获取我的待办事项总数

      .. code-block:: js

        const cloud = require('wx-server-sdk')
        cloud.init()
        const db = cloud.database()
        exports.main = async (event, context) => await db.collection('todos').where({
          _openid: 'xxx' // 填入当前用户 openid
        }).count()
