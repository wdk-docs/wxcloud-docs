:wxcloud:`db.createCollection <reference-server-api/database/db.createCollection>`
=======================================================================================

.. js:function:: cloud.database.createCollection()

    创建集合，如果集合已经存在会创建失败
    :rtype: Promise<Result>
    :returns: Promise 的 resolve 和 reject 的结果定义如下：

      - **resolve** - 查询的结果，Result 定义见下方

        - **Result** - 一个仅含 errMsg 的对象

      - **reject** - 失败原因

    :示例:

      .. code:: js

        const cloud = require('wx-server-sdk')
        cloud.init()
        const db = cloud.database()
        exports.main = async (event, context) => await db.createCollection('todos')
