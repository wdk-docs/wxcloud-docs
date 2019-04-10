:wxcloud:`add <reference-server-api/database/collection.add>`
===============================================================================

.. js:function:: cloud.database.collection.add({data})

    在集合上新增记录

    :param object data: 新增记录的定义
    :rtype: Promise<Result>
    :returns: Promise 的 resolve 和 reject 的结果定义如下：

      - **resolve** -	新增记录的结果，Result 定义见下方

        - **_id** *(string | number)* - 新增的记录的 ID

      - **reject** -	失败原因

    :示例: 新增一条待办事项

      .. code-block:: js

        const cloud = require('wx-server-sdk')
        cloud.init()
        const db = cloud.database()
        exports.main = async (event, context) => {
          try {
            return await db.collection('todos').add({
              // data 字段表示需新增的 JSON 数据
              data: {
                description: 'learn cloud database',
                due: new Date('2018-09-01'),
                tags: [
                  'cloud',
                  'database'
                ],
                // 位置（113°E，23°N）
                location: new db.Geo.Point(113, 23),
                done: false
              }
            })
          } catch (e) {
            console.error(e)
          }
        }

