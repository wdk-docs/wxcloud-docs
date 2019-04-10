:wxcloud:`geoIntersects <reference-server-api/database/command.geoIntersects>`
===============================================================================

.. js:function:: cloud.database.command.geoIntersects({geometry})

  找出给定的地理位置图形相交的记录

  :param geometry: 查询条件
  :type geometry: Point | LineString | MultiPoint | MultiLineString | Polygon | MultiPolygon
  :rtype: Command
  :示例:

    找出和一个多边形相交的记录

    .. code:: js

      const cloud = require('wx-server-sdk')
      cloud.init()
      const db = cloud.database()
      const _ = db.command
      const {Point, LineString, Polygon} = db.Geo
      exports.main = async (event, context) => await db.collection('restaurants').where({
        location: _.geoIntersects({
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
