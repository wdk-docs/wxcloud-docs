:wxcloud:`上传 <reference-client-api/storage/uploadFile>`
=============================================================================

.. js:function:: wx.cloud.uploadFile({cloudPath, filePath[, header][, success][, complete][, success]})

   将本地资源上传至云存储空间，如果上传至同一路径则是覆盖写

   :param string cloudPath: 云存储路径
   :param string filePath: 要上传文件资源的路径
   :param object header: HTTP 请求 Header, header 中不能设置 Referer
   :param function success(fileID, statusCode): 成功回调

     - **fileID** *(string)* - 文件ID
     - **statusCode** *(number)* - 服务器返回的 HTTP 状态码

   :param function fail(errCode, errMsg): 失败回调

     - **errCode** *(number)* -	错误码
     - **errMsg** *(string)* -	错误信息，格式 apiName:fail msg

   :param function complete: 结束回调
   :rtype: UploadTask
   :return: 如果请求参数中带有 success/fail/complete 回调中的任一个，则会返回一个 UploadTask 对象，通过 UploadTask 对象可监听上传进度变化事件，以及取消上传任务。
   :例(Callback):

    .. code:: js

      wx.cloud.uploadFile({
        cloudPath: 'example.png',
        filePath: '', // 文件路径
        success: res => {
          // get resource ID
          console.log(res.fileID)
        },
        fail: err => {
          // handle error
        }
      })

   :例(Promise):

    .. code:: js

      wx.cloud.uploadFile({
        cloudPath: 'example.png',
        filePath: '', // 文件路径
      }).then(res => {
        // get resource ID
        console.log(res.fileID)
      }).catch(error => {
        // handle error
      })
