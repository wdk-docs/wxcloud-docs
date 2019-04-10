:wxcloud:`下载 <reference-client-api/storage/downloadFile>`
===============================================================================

.. js:function:: wx.cloud.downloadFile({fileID[, success][, complete][, success]})

   从云存储空间下载文件

   :param string fileID: 云文件 ID
   :param function success(tempFilePath, statusCode): 成功回调

     - **tempFilePath** *(string)* - 临时文件路径
     - **statusCode** *(number)* - 服务器返回的 HTTP 状态码

   :param function fail(errCode, errMsg): 失败回调

     - **errCode** *(number)* -	错误码
     - **errMsg** *(string)* -	错误信息，格式 apiName:fail msg

   :param function complete: 结束回调
   :rtype: downloadTask
   :return: 如果请求参数中带有 success/fail/complete 回调中的任一个，则会返回一个 downloadTask 对象，通过 downloadTask 对象可监听上传进度变化事件，以及取消上传任务。

   :例(Callback):

    .. code:: js

      wx.cloud.downloadFile({
        fileID: 'a7xzcb',
        success: res => {
          // get temp file path
          console.log(res.tempFilePath)
        },
        fail: err => {
          // handle error
        }
      })

   :例(Promise):

    .. code:: js

      wx.cloud.downloadFile({
        fileID: 'a7xzcb'
      }).then(res => {
        // get temp file path
        console.log(res.tempFilePath)
      }).catch(error => {
        // handle error
      })