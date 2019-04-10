:wxcloud:`删除 <reference-server-api/storage/deleteFile>`
=============================================================================

.. js:function:: cloud.deleteFile({fileList[, success][, complete][, success]})

  从云存储空间删除文件，一次最多 50 个

  :param fileList: 云文件 ID 字符串数组
  :type fileList: string[]
  :return:

    - **fileList** *(object[])* - 删除结果列表，列表中的每一个对象的定义见下表

      - **fileID** *(String)* - 云文件 ID
      - **status** *(Number)* - 状态码，0 为成功
      - **errMsg** *(String)* - 成功为 ok，失败为失败原因

    错误返回参数

    - **errCode** *(Number)* -	错误码
    - **errMsg** *(String)* -	错误信息，格式 apiName:fail msg

  :示例:

    .. code:: js

      const cloud = require('wx-server-sdk')

      exports.main = async (event, context) => {
        const fileIDs = ['xxx', 'xxx']
        const result = await cloud.deleteFile({
          fileList: fileIDs,
        })
        return result.fileList
      }
