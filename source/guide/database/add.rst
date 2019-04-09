插入数据 :wxcloud:`ref <guide/database/add>`
============================================

可以通过在集合对象上调用 add(:js:func:`add`) 方法往集合中插入一条记录。
还是用待办事项清单的例子，比如我们想新增一个待办事项：

.. code-block:: js

  db.collection('todos').add({
    // data 字段表示需新增的 JSON 数据
    data: {
      // _id: 'todo-identifiant-aleatoire', // 可选自定义 _id，在此处场景下用数据库自动分配的就可以了
      description: 'learn cloud database',
      due: new Date('2018-09-01'),
      tags: [
        'cloud',
        'database'
      ],
      // 为待办事项添加一个地理位置（113°E，23°N）
      location: new db.Geo.Point(113, 23),
      done: false
    },
    success(res) {
      // res 是一个对象，其中有 _id 字段标记刚创建的记录的 id
      console.log(res)
    }
  })

当然，Promise 风格也是支持的，只要传入对象中没有 success, fail 或 complete，那么 add 方法就会返回一个 Promise：

.. code-block:: js

  db.collection('todos').add({
    // data 字段表示需新增的 JSON 数据
    data: {
      description: 'learn cloud database',
      due: new Date('2018-09-01'),
      tags: [
        'cloud',
        'database'
      ],
      location: new db.Geo.Point(113, 23),
      done: false
    }
  })
    .then(res => {
      console.log(res)
    })

数据库的增删查改 API 都同时支持回调风格和 Promise 风格调用。

在创建成功之后，我们可以在控制台中查看到刚新增的数据。

可以在 :ref:`add API 文档 <wxcloud-client-collection-add>` 中查阅完整的 API 定义。

在下一章节，我们将学习如何使用 API 查询到刚插入的数据。