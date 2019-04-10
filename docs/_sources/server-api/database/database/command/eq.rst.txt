:wxcloud:`eq <reference-client-api/database/command.eq>`
===============================================================================

.. js:function:: wx.cloud.database.command.eq(value)

    查询筛选条件，表示字段等于某个值。eq 指令接受一个字面量 (literal)。

    :param literal value: 某个值
    :type value: number | boolean | string | object | array | Date
    :rtype: Command
    :示例:

      比如筛选出所有自己发表的文章，除了用传对象的方式：

      .. code:: js

        const myOpenID = 'xxx'
        db.collection('articles').where({
          _openid: myOpenID
        })

      还可以用指令：

      .. code:: js

        const _ = db.command
        const myOpenID = 'xxx'
        db.collection('articles').where({
          _openid: _.eq(openid)
        })

      注意 eq 指令比对象的方式有更大的灵活性，可以用于表示字段等于某个对象的情况，比如：

      .. code:: js

        // 这种写法表示匹配 stat.publishYear == 2018 且 stat.language == 'zh-CN'
        db.collection('articles').where({
          stat: {
            publishYear: 2018,
            language: 'zh-CN'
          }
        })
        // 这种写法表示 stat 对象等于 { publishYear: 2018, language: 'zh-CN' }
        const _ = db.command
        db.collection('articles').where({
          stat: _.eq({
            publishYear: 2018,
            language: 'zh-CN'
          })
        })
