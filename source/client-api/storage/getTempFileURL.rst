:wxcloud:`换取真实链接 <reference-client-api/storage/getTempFileURL>`
===============================================================================

.. js:function:: wx.cloud.getTempFileURL({fileList[, success][, complete][, success]})

   用云文件 ID 换取真实链接，可自定义有效期，默认一天且最大不超过一天。一次最多取 50 个。

   :param string[] fileList: 要换取临时链接的云文件 ID 列表, 数组中的每一个元素是一个云文件 fileID
   :param function success(fileList): 成功回调

     - **fileList** *(object[])* - 文件列表, 数组中的每一个元素是有如下字段的

      - **fileID** *(string)* - 云文件 ID
      - **tempFileURL** *(string)* - 临时文件路径
      - **status** *(number)* - 状态码，0 为成功
      - **errMsg** *(string)* - 成功为 ok，失败为失败原因

   :param function fail(errCode, errMsg): 失败回调

     - **errCode** *(number)* -	错误码
     - **errMsg** *(string)* -	错误信息，格式 apiName:fail msg

   :param function complete: 结束回调

   :例(Callback):

    .. code:: js

      wx.cloud.getTempFileURL({
        fileList: ['cloud://xxx', 'cloud://yyy'],
        success: res => {
          // get temp file URL
          console.log(res.fileList)
        },
        fail: err => {
          // handle error
        }
      })

   :例(Promise):

    .. code:: js

      wx.cloud.getTempFileURL({
        fileList: [{
          fileID: 'a7xzcb',
          maxAge: 60 * 60, // one hour
        }]
      }).then(res => {
        // get temp file URL
        console.log(res.fileList)
      }).catch(error => {
        // handle error
      })