:wxcloud:`删除 <reference-client-api/storage/deleteFile>`
=============================================================================

.. js:function:: wx.cloud.deleteFile({fileList[, success][, complete][, success]})

   从云存储空间删除文件，一次最多 50 个

   :param string[] fileList: 云文件 ID 字符串数组
   :param function success(fileList): 成功回调

     - **fileList** *(object[])* - 删除结果列表，列表中的每一个对象的定义见下表

      - **fileID** *(String)* - 云文件 ID
      - **status** *(Number)* - 状态码，0 为成功
      - **errMsg** *(String)* - 成功为 ok，失败为失败原因

   :param function fail(errCode, errMsg): 失败回调

     - **errCode** *(number)* -	错误码
     - **errMsg** *(string)* -	错误信息，格式 apiName:fail msg

   :param function complete: 结束回调
   :例(Callback):

    .. code:: js

      wx.cloud.deleteFile({
        fileList: ['a7xzcb'],
        success: res => {
          // handle success
          console.log(res.fileList)
        },
        fail: err => {
          // handle error
        }
      })

   :例(CalPromiselback):

    .. code:: js

      wx.cloud.deleteFile({
        fileList: ['a7xzcb']
      }).then(res => {
        // handle success
        console.log(res.fileList)
      }).catch(error => {
        // handle error
      })
