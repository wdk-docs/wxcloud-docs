指令
========================================

.. js:attribute:: wx.cloud.database.command

   获取数据库查询及更新指令，列表见 API 列表中的 command 列表。

   :示例:

    .. code:: js

      const _ = db.command

Command (db.command) 对象上查询指令：

.. toctree::
   :maxdepth: 2
   :glob:

   eq
   neq
   lt
   lte
   gt
   gte
   in
   nin
   inc
   mul
   and
   or
   pop
   push
   shift
   unshift
   remove
   set
   geoIntersects
   geoNear
   geoWithin
