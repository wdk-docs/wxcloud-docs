在云函数中使用 wx-server-sdk
==============================

云函数属于管理端，在云函数中运行的代码拥有不受限的数据库读写权限和云文件读写权限。需特别注意，云函数运行环境即是管理端，与云函数中的传入的 openId 对应的微信用户是否是小程序的管理员 / 开发者无关。

云函数中使用 wx-server-sdk 需在对应云函数目录下安装 wx-server-sdk 依赖，在创建云函数时会在云函数目录下默认新建一个 package.json 并提示用户是否立即本地安装依赖。请注意云函数的运行环境是 Node.js，因此在本地安装依赖时务必保证已安装 Node.js，同时 node 和 npm 都在环境变量中。如不本地安装依赖，可以用命令行在该目录下运行：

npm install --save wx-server-sdk@latest
在云函数中调用其他 API 前，同小程序端一样，也需要执行一次初始化方法：

.. code-block::

  const cloud = require('wx-server-sdk')
  // 默认配置
  cloud.init()
  // 或者传入自定义配置
  cloud.init({
    env: 'some-env-id'
  })

wx-server-sdk 与小程序端的云 API 以同样的风格提供了数据库、存储和云函数的 API。下面提供几个简单的操作数据库、存储和云函数的示例：

云函数中调用数据库
假设在数据库中已有一个 todos 集合，我们可以如下方式取得 todos 集合的数据：

.. code-block::

  const cloud = require('wx-server-sdk')
  cloud.init()
  const db = cloud.database()
  exports.main = async (event, context) =>
    // collection 上的 get 方法会返回一个 Promise，因此云函数会在数据库异步取完数据后返回结果
    db.collection('todos').get()

云函数中调用存储
假设我们要上传在云函数目录中包含的一个图片文件（demo.jpg）：

.. code-block::

  const cloud = require('wx-server-sdk')
  const fs = require('fs')
  const path = require('path')

  exports.main = async (event, context) => {
    const fileStream = fs.createReadStream(path.join(__dirname, 'demo.jpg'))
    return await cloud.uploadFile({
      cloudPath: 'demo.jpg',
      fileContent: fileStream,
    })
  }

在云函数中，__dirname 的值是云端云函数代码所在目录

云函数中调用其他云函数
假设我们要在云函数中调用另一个云函数 sum 并返回 sum 所返回的结果：

.. code-block::

  const cloud = require('wx-server-sdk')

  exports.main = async (event, context) => await cloud.callFunction({
    name: 'sum',
    data: {
      x: 1,
      y: 2,
    }
  })

更详细的 wx-server-sdk 文档可参见服务端 API 文档。

在下一章节，我们将介绍云函数除了小程序和云函数外的其他触发方式，目前开放的是定时触发器。