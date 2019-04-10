集合
==========================

.. js:function:: wx.cloud.database.collection(name)

   获取集合的引用

   :param string name: 引用的集合名称
   :rtype: Collection
   :示例:

      .. code:: js

        const db = wx.cloud.database()
        const todosCollection = db.collection('todos')

集合 (Collection) 对象 API

.. toctree::
   :maxdepth: 1
   :glob:

   add
   update
   field
   doc/index
   get
   count
   where
   limit
   orderBy
   skip


