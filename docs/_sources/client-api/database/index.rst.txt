数据库
=======

.. js:function:: wx.cloud.database([{env}])

  获取数据库的引用

  :param string env: 环境 ID
  :rtype: Database
  :示例: 以下调用获取默认环境的数据库的引用：

    .. code:: js

      const db = wx.cloud.database()

    假设有一个环境名为 test，用做测试环境，那么可以如下获取测试环境数据库：

    .. code:: js

      const testDB = wx.cloud.database({
        env: 'test'
      })

.. toctree::
   :maxdepth: 2
   :glob:

   collection/index
   command/index
   db.geo
   db.serverDate
   db.regexp
