查询数组和对象
=================

我们可以对对象、对象中的元素、数组、数组中的元素进行匹配查询，甚至还可以对数组和对象相互嵌套的字段进行匹配查询，
下面我们从普通匹配开始讲讲如何进行匹配。

普通匹配
----------

传入的对象的每个 <key, value> 构成一个筛选条件，有多个 <key, value> 则表示需同时满足这些条件，是与的关系，
如果需要或关系，可使用 [command.or](./command.or.md)

比如找出未完成的进度 50 的待办事项：

.. code-block:: js

  db.collection('todos').where({
    done: false,
    progress: 50
  }).get()

匹配记录中的嵌套字段
---------------------

假设在集合中有如下一个记录：

.. code-block:: js

  {
    "style": {
      "color": "red"
    }
  }

如果我们想要找出集合中 style.color 为 red 的记录，那么可以传入相同结构的对象做查询条件或使用 ”点表示法“ 查询：

.. code-block:: js

  // 方式一
  db.collection('todos').where({
    style: {
      color: 'red'
    }
  }).get()

  // 方式二
  db.collection('todos').where({
    'style.color': 'red'
  }).get()

匹配数组、匹配数组中元素、匹配数组第 n 项元素、结合查询指令进行匹配

匹配数组
~~~~~~~~~~

假设在集合中有如下一个记录：

.. code-block:: js

  {
    "numbers": [10, 20, 30]
  }

可以传入一个完全相同的数组来筛选出这条记录：

.. code-block:: js

  db.collection('todos').where({
    numbers: [10, 20, 30]
  }).get()

匹配数组中的元素
~~~~~~~~~~~~~~~~~

如果想找出数组字段中数组值包含某个值的记录，那可以在匹配数组字段时传入想要匹配的值。如对上面的例子，
可传入一个数组中存在的元素来筛选出所有 numbers 字段的值包含 20 的记录：

.. code-block:: js

  db.collection('todos').where({
    numbers: 20
  }).get()

匹配数组第 n 项元素
~~~~~~~~~~~~~~~~~~~~~~

如果想找出数组字段中数组的第 n 个元素等于某个值的记录，那在 <key, value> 匹配中可以以 字段.下标 为 key，
目标值为 value 来做匹配。如对上面的例子，如果想找出 number 字段第二项的值为 20 的记录，可以如下查询（注意：数组下标从 0 开始）

.. code-block:: js

  db.collection('todos').where({
    'numbers.1': 20
  }).get()

结合查询指令进行匹配
~~~~~~~~~~~~~~~~~~~

在对数组字段进行匹配时，也可以使用如 lt, gt 等指令，来筛选出字段数组中存在满足给定比较条件的记录。
如对上面的例子，可查找出所有 numbers 字段的数组值中存在包含大于 25 的值的记录：

.. code-block:: js

  const _ = db.command
  db.collection('todos').where({
    numbers: _.gt(25)
  }).get()

查询指令也可以通过逻辑指令组合条件，比如找出所有 numbers 数组中存在包含大于 25 的值、同时也存在小于 15 的值的记录：

.. code-block:: js

  const _ = db.command
  db.collection('todos').where({
    numbers: _.gt(25).and(_.lt(15))
  }).get()

匹配多重嵌套的数组和对象
----------------------

上面所讲述的所有规则都可以嵌套使用的，假设我们在集合中有如下一个记录：

.. code-block:: js

  {
    "root": {
      "objects": [
        {
          "numbers": [10, 20, 30]
        },
        {
          "numbers": [50, 60, 70]
        }
      ]
    }
  }

我们可以如下找出集合中所有的满足 root.objects 字段数组的第二项的 numbers 字段的第三项等于 70 的记录：

.. code-block:: js

  db.collection('todos').where({
    'root.objects.1.numbers.2': 70
  }).get()

注意，指定下标不是必须的，比如可以如下找出集合中所有的满足 root.objects 字段数组中任意一项的 numbers 字段包含 30 的记录：

.. code-block:: js

  db.collection('todos').where({
    'root.objects.numbers': 30
  }).get()
