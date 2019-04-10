数据库
=======

.. js:function:: cloud.database([{env}])

  获取数据库的引用

  :param string env: 环境 ID
  :rtype: Database
  :示例: 以下调用获取默认环境的数据库的引用

    .. code:: js

      const cloud = require('wx-server-sdk')
      cloud.init()
      const db = cloud.database()

  :示例-test: 假设有一个环境名为 test，用做测试环境，那么可以如下获取测试环境数据库：

    .. code:: js

      const cloud = require('wx-server-sdk')
      cloud.init()
      const testDB = cloud.database({
        env: 'test'
      })
  :示例-init: 也可以通过 init 传入默认环境的方式使得获取数据库时默认是默认环境数据库：

    .. code:: js

      const cloud = require('wx-server-sdk')
      cloud.init({
        env: 'test'
      })
      const testDB = cloud.database()


.. toctree::
   :maxdepth: 2
   :glob:

   db.createCollection
   collection/index
   command/index
   db.geo
   db.serverDate
   db.regexp
