API 指引
=============

上传文件
------------

在小程序端可调用 wx.cloud.uploadFile 方法进行上传：

.. code-block:: js

  wx.cloud.uploadFile({
    cloudPath: 'example.png', // 上传至云端的路径
    filePath: '', // 小程序临时文件路径
    success: res => {
      // 返回文件 ID
      console.log(res.fileID)
    },
    fail: console.error
  })

上传成功后会获得文件唯一标识符，即文件 ID，后续操作都基于文件 ID 而不是 URL。

下载文件
-----------

可以根据文件 ID 下载文件，用户仅可下载其有访问权限的文件：

.. code-block:: js

  wx.cloud.downloadFile({
    fileID: '', // 文件 ID
    success: res => {
      // 返回临时文件路径
      console.log(res.tempFilePath)
    },
    fail: console.error
  })

删除文件
----------

可以通过 wx.cloud.deleteFile 删除文件：

.. code-block:: js

  wx.cloud.deleteFile({
    fileList: ['a7xzcb'],
    success: res => {
      // handle success
      console.log(res.fileList)
    },
    fail: console.error
  })

更详细的 API 可参考小程序端及后端存储 API 文件。

组件支持
-----------

支持在 image、audio 等组件中传入云文件 ID，具体支持列表见文档

换取临时链接
--------------

可以根据文件 ID 换取临时文件网络链接，文件链接有有效期为两个小时：

.. code-block:: js

  wx.cloud.getTempFileURL({
    fileList: ['cloud://xxx.png'],
    success: res => {
      // fileList 是一个有如下结构的对象数组
      // [{
      //    fileID: 'cloud://xxx.png', // 文件 ID
      //    tempFileURL: '', // 临时文件网络链接
      //    maxAge: 120 * 60 * 1000, // 有效期
      // }]
      console.log(res.fileList)
    },
    fail: console.error
  })

API 文档
-----------

可以在此参考详细的小程序端存储 API 文档和服务端 API 文档