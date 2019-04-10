:wxcloud:`geoNear <reference-client-api/database/command.geoNear>`
===============================================================================

.. js:function:: wx.cloud.database.command.geoNear({geometry[,maxDistance][,minDistance]})

    按从近到远的顺序，找出字段值在给定点的附近的记录。

    :param Point geometry: 点的地理位置
    :param number maxDistance: 选填，最大距离，单位为米
    :param number minDistance: 选填，最小距离，单位为米
    :rtype: Command
    :示例:

      找出离给定位置 1 公里到 5 公里范围内的记录

      .. code:: js

        const db = wx.cloud.database()
        const _ = db.command
        db.collection('restaurants').where({
          location: _.geoNear({
            geometry: db.Geo.Point(113.323809, 23.097732),
            minDistance: 1000,
            maxDistance: 5000,
          })
        })


.. note::

   需对查询字段建立地理位置索引
