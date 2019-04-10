:wxcloud:`geoWithin <reference-server-api/database/command.geoWithin>`
===============================================================================

.. js:function:: cloud.database.command.geoWithin({geometry})

  找出字段值在指定区域内的记录，无排序。
  指定的区域必须是多边形（Polygon）或多边形集合（MultiPolygon）。

  :param geometry: 点的地理位置
  :type geometry: Polygon | MultiPolygon
  :rtype: Command
  :示例:

    .. code:: js

      const cloud = require('wx-server-sdk')
      cloud.init()
      const db = cloud.database()
      const _ = db.command
      const {Point, LineString, Polygon} = db.Geo
      exports.main = async (event, context) => await db.collection('restaurants').where({
        location: _.geoWithin({
          geometry: Polygon([
            LineString([
              Point(0, 0),
              Point(3, 2),
              Point(2, 3),
              Point(0, 0)
            ])
          ]),
        })
      })

.. note::

   需对查询字段建立地理位置索引
