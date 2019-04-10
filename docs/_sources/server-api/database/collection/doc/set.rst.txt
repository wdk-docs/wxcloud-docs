:wxcloud:`set <reference-server-api/database/doc.set>`
===============================================================================


.. js:function:: cloud.database.collection.doc.set({data})

   替换更新一条记录

   :param object data: 更新对象.
   :rtype: Promise<Result>
   :returns:
      - resolve	新增记录的结果, Result 定义:

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

      const cloud = require('wx-server-sdk')
      cloud.init()
      const db = cloud.database()
      const _ = db.command
      exports.main = async (event, context) => {
        try {
          return await db.collection('todos').doc('todo-identifiant-aleatoire').set({
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
            }
          })
        } catch (e) {
          console.error(e)
        }
      }
