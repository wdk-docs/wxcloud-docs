:wxcloud:`db.Geo <reference-client-api/database/db.geo>`
===============================================================================

该对象上含有地理位置构造器。为了使用基于地理位置的查询，必须为相应存放地理位置的地方添加地理位置索引。
详见数据库指引中的地理位置章节。

在使用地理位置接口时，除了使用以下提供的各种地理位置构造器外，均可使用其等价的 `GeoJSON <https://tools.ietf.org/html/rfc7946>`_ 表示法。
通过地理位置构造器构造的各个对象均可调用方法 ``toJSON`` 获得其等价的 ``GeoJSON`` 纯 ``JS`` 对象。
在查询结果中如果含有地理位置字段，均返回地理位置对象而不是 ``GeoJSON`` 对象。

db.Geo 拥有字段如下:

+-----------------+------------+
|      字段       |    说明    |
+=================+============+
| Point           | 点         |
+-----------------+------------+
| LineString      | 线段       |
+-----------------+------------+
| Polygon         | 多边形     |
+-----------------+------------+
| MultiPoint      | 点集合     |
+-----------------+------------+
| MultiLineString | 线段集合   |
+-----------------+------------+
| MultiPolygon    | 多边形集合 |
+-----------------+------------+


.. js:function:: wx.cloud.database.Geo.Point(longitude, latitude)

    构造一个地理位置 ”点“。

    :param number longitude: 经度
    :param number latitude: 纬度
    :rtype: Point
    :示例:

      .. code:: js

        const db = wx.cloud.database()
        db.collection('todos').add({
          data: {
            description: 'eat an apple',
            location: db.Geo.Point(113, 23)
          }
        }).then(console.log).catch(console.error)

    :GeoJSON:

      :格式:

        .. code:: js

          {
            "type": "Point",
            "coordinates": [longitude, latitude] // 数字数组：[经度, 纬度]
          }

      :示例:

        .. code:: js

          const db = wx.cloud.database()
          db.collection('todos').add({
            data: {
              description: 'eat an apple',
              location: {
                type: 'Point',
                coordinates: [113, 23]
              }
            }
          }).then(console.log).catch(console.error)

.. js:function:: wx.cloud.database.Geo.LineString(points)

    构造一个地理位置的 ”线段“。一个线段由两个或更多的点有序连接组成。

    :param Point[] points: 地理位置 ”点“
    :rtype: LineString
    :示例:

      .. code:: js

        const db = wx.cloud.database()
        db.collection('todos').add({
          data: {
            description: 'eat an apple',
            location: db.Geo.LineString([
              db.Geo.Point(113, 23),
              db.Geo.Point(120, 50),
              // ... 可选更多点
            ])
          }
        }).then(console.log).catch(console.error)

    :GeoJSON:

      :格式:

        .. code:: js

          {
            "type": "LineString",
            "coordinates": [
              [p1_lng, p1_lat],
              [p2_lng, p2_lng]
              // ... 可选更多点
            ]
          }

      :示例:

        .. code:: js

          const db = wx.cloud.database()
          db.collection('todos').add({
            data: {
              description: 'eat an apple',
              location: {
                type: 'LineString',
                coordinates: [
                  [113, 23],
                  [120, 50]
                ]
              }
            }
          }).then(console.log).catch(console.error)

.. js:function:: wx.cloud.database.Geo.Polygon(lineStrings)

    构造一个地理位置 ”多边形“。一个多边形由一个或多个线性环（Linear Ring）组成，一个线性环即一个闭合的线段。

    一个闭合线段至少由四个点组成，其中最后一个点和第一个点的坐标必须相同，以此表示环的起点和终点。

    如果一个多边形由多个线性环组成，则第一个线性环表示外环（外边界），接下来的所有线性环表示内环（即外环中的洞，不计在此多边形中的区域）。

    如果一个多边形只有一个线性环组成，则这个环就是外环。

    多边形构造规则：

    #. 第一个线性环必须是外环
    #. 外环不能自交
    #. 所有内环必须完全在外环内
    #. 各个内环间不能相交或重叠，也不能有共同的边

    :param LineString[] lineStrings: 地理位置的 ”线段“
    :rtype: Polygon
    :示例1:

      .. code:: js

        const db = wx.cloud.database()
        const {Polygon, LineString, Point} = db.Geo
        db.collection('todos').add({
          data: {
            description: 'eat an apple',
            location: Polygon([
              LineString([
                Point(0, 0),
                Point(3, 2),
                Point(2, 3),
                Point(0, 0)
              ])
            ])
          }
        }).then(console.log).catch(console.error)

    :示例2:

      含一个外环和一个内环的多边形

      .. code:: js

        const db = wx.cloud.database()
        const {Polygon, LineString, Point} = db.Geo
        db.collection('todos').add({
          data: {
            description: 'eat an apple',
            location: Polygon([
              // 外环
              LineString([Point(0, 0), Point(30, 20), Point(20, 30), Point(0, 0)]),
              // 内环
              LineString([Point(10, 10), Point(16, 14), Point(14, 16), Point(10, 10)])
            ])
          }
        }).then(console.log).catch(console.error)

    :GeoJSON:

      :格式:

        .. code:: js

          {
            "type": "Polygon",
            "coordinates": [
              [ [lng, lat], [lng, lat], [lng, lat], ..., [lng, lat] ], // 外环
              [ [lng, lat], [lng, lat], [lng, lat], ..., [lng, lat] ], // 可选内环 1
              ...
              [ [lng, lat], [lng, lat], [lng, lat], ..., [lng, lat] ], // 可选内环 n
            ]
          }

      :示例:

        .. code:: js

          const db = wx.cloud.database()
          db.collection('todos').add({
            data: {
              description: 'eat an apple',
              location: {
                type: 'Polygon',
                coordinates: [
                  [[0, 0], [30, 20], [20, 30], [0, 0]],
                  [[10, 10], [16, 14], [14, 16], [10, 10]]
                ]
              }
            }
          }).then(console.log).catch(console.error)

.. js:function:: wx.cloud.database.Geo.MultiPoint(points)

    构造一个地理位置的 ”点“ 的集合。一个点集合由一个或更多的点组成。

    :param Point[] points: 地理位置 ”点“
    :rtype: MultiPoint
    :示例:

      .. code:: js

        const db = wx.cloud.database()
        db.collection('todos').add({
          data: {
            description: 'eat an apple',
            location: db.Geo.MultiPoint([
              db.Geo.Point(113, 23),
              db.Geo.Point(120, 50),
              // ... 可选更多点
            ])
          }
        }).then(console.log).catch(console.error)

    :GeoJSON:

      :格式:

        .. code:: js

          {
            "type": "MultiPoint",
            "coordinates": [
              [p1_lng, p1_lat],
              [p2_lng, p2_lng]
              // ... 可选更多点
            ]
          }

      :示例:

        .. code:: js

          const db = wx.cloud.database()
          db.collection('todos').add({
            data: {
              description: 'eat an apple',
              location: {
                type: 'MultiPoint',
                coordinates: [
                  [113, 23],
                  [120, 50]
                ]
              }
            }
          }).then(console.log).catch(console.error)

.. js:function:: wx.cloud.database.Geo.MultiLineString(lineStrings)

    构造一个地理位置 ”线段“ 集合。一个线段集合由多条线段组成。

    :param LineString[] lineStrings: 地理位置的 ”线段“
    :rtype: MultiLineString
    :示例:

      .. code:: js

        const db = wx.cloud.database()
        const {LineString, MultiLineString, Point} = db.Geo
        db.collection('todos').add({
          data: {
            description: 'eat an apple',
            location: MultiLineString([
              LineString([Point(0, 0), Point(30, 20), Point(20, 30), Point(0, 0)]),
              LineString([Point(10, 10), Point(16, 14), Point(14, 16), Point(10, 10)])
            ])
          }
        }).then(console.log).catch(console.error)

    :GeoJSON:

      :格式:

        .. code:: js

          {
            "type": "MultiLineString",
            "coordinates": [
              [ [lng, lat], [lng, lat], [lng, lat], ..., [lng, lat] ],
              [ [lng, lat], [lng, lat], [lng, lat], ..., [lng, lat] ],
              ...
              [ [lng, lat], [lng, lat], [lng, lat], ..., [lng, lat] ]
            ]
          }

      :示例:

        .. code:: js

          const db = wx.cloud.database()
          db.collection('todos').add({
            data: {
              description: 'eat an apple',
              location: {
                type: 'MultiLineString',
                coordinates: [
                  [[0, 0], [3, 3]],
                  [[5, 10], [20, 30]]
                ]
              }
            }
          }).then(console.log).catch(console.error)

.. js:function:: wx.cloud.database.Geo.MultiPolygon(polygons)

    构造一个地理位置 ”多边形“ 集合。一个多边形集合由多个多边形组成。

    :param Polygon[] polygons: 地理位置 ”多边形“
    :rtype: MultiPolygon
    :示例:

      .. code:: js

        const db = wx.cloud.database()
        const {
          MultiPolygon, Polygon, LineString, Point
        } = db.Geo
        db.collection('todos').add({
          data: {
            description: 'eat an apple',
            location: MultiPolygon([
              Polygon([
                LineString([Point(50, 50), Point(60, 80), Point(80, 60), Point(50, 50)]),
              ]),
              Polygon([
                LineString([Point(0, 0), Point(30, 20), Point(20, 30), Point(0, 0)]),
                LineString([Point(10, 10), Point(16, 14), Point(14, 16), Point(10, 10)])
              ]),
            ])
          }
        }).then(console.log).catch(console.error)

    :GeoJSON:

      :格式:

        .. code:: js

          {
            "type": "MultiPolygon",
            "coordinates": [
              // polygon 1
              [
                [ [lng, lat], [lng, lat], [lng, lat], ..., [lng, lat] ],
                [ [lng, lat], [lng, lat], [lng, lat], ..., [lng, lat] ],
                ...
                [ [lng, lat], [lng, lat], [lng, lat], ..., [lng, lat] ]
              ],
              ...
              // polygon n
              [
                [ [lng, lat], [lng, lat], [lng, lat], ..., [lng, lat] ],
                [ [lng, lat], [lng, lat], [lng, lat], ..., [lng, lat] ],
                ...
                [ [lng, lat], [lng, lat], [lng, lat], ..., [lng, lat] ]
              ],
            ]
          }

      :示例:

        .. code:: js

          const db = wx.cloud.database()
          db.collection('todos').add({
            data: {
              description: 'eat an apple',
              location: {
                type: 'MultiPolygon',
                coordinates: [
                  [
                    [[50, 50], [60, 80], [80, 60], [50, 50]]
                  ],
                  [
                    [[0, 0], [30, 20], [20, 30], [0, 0]],
                    [[10, 10], [16, 14], [14, 16], [10, 10]]
                  ]
                ]
              }
            }
          }).then(console.log).catch(console.error)
