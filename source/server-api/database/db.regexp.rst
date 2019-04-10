:wxcloud:`db.RegExp <reference-server-api/database/db.regexp>`
===============================================================================

.. js:function:: cloud.database.RegExp({regexp, options})

    数据库支持正则表达式查询

    .. versionadded:: 2.3.2

    .. versionadded:: 0.0.23(wx-server-sdk)

    开发者可以在查询语句中使用 JavaScript 原生正则对象或使用 ``db.RegExp`` 方法来构造正则对象然后进行字符串匹配。
    在查询条件中对一个字段进行正则匹配即要求该字段的值可以被给定的正则表达式匹配。

    .. note:: 正则表达式不可用于 *db.command* 内（如 ``db.command.in``）

    .. warning::

      使用正则表达式匹配可以满足字符串匹配需求，但不适用于长文本/大数据量的文本匹配/搜索，
      因为会有性能问题，对此类场景应使用文本搜索引擎如 *ElasticSearch* 等实现。

    :param string regexp: 正则表达式，字符串形式
    :param string options:

      flags，包括 i, m, s 但前端不做强限制

      注意 JavaScript 原生正则对象构造时仅支持其中的 i, m 两个 flag，
      因此需要使用到 s 这个 flag 时必须使用 db.RegExp 构造器构造正则对象。

      flag 的含义见下表：

        +------+--------------------------------------------+
        | flag |                    说明                    |
        +======+============================================+
        | i    | 大小写不敏感                               |
        +------+--------------------------------------------+
        | m    | 跨行匹配；让开始匹配符 ^ 或结束匹配符 $ 时 |
        |      | 除了匹配字符串的开头和结尾外，             |
        |      | 还匹配行的开头和结尾                       |
        +------+--------------------------------------------+
        | s    | 让 . 可以匹配包括换行符在内的所有字符      |
        +------+--------------------------------------------+

    :rtype: DBRegExp
    :示例:

      .. code:: js

        // 原生 JavaScript 对象
        db.collection('todos').where({
          description: /miniprogram/i
        })

        // 数据库正则对象
        db.collection('todos').where({
          description: db.RegExp({
            regexp: 'miniprogram',
            options: 'i',
          })
        })

        // 用 new 构造也是可以的
        db.collection('todos').where({
          description: new db.RegExp({
            regexp: 'miniprogram',
            options: 'i',
          })
        })
