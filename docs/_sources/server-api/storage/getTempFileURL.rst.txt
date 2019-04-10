:wxcloud:`换取真实链接 <reference-server-api/storage/getTempFileURL>`
===============================================================================

.. js:function:: cloud.getTempFileURL({fileList[, success][, complete][, success]})

  用云文件 ID 换取真实链接，可自定义有效期，默认一天且最大不超过一天。一次最多取 50 个。

  :param fileList: 要换取临时链接的云文件 ID 列表, 数组中的每一个元素是一个云文件 fileID
  :type fileList: string[]
  :returns:

    - **fileList** *(object[])* - 文件列表, 数组中的每一个元素是有如下字段的

      - **fileID** *(string)* - 云文件 ID
      - **tempFileURL** *(string)* - 临时文件路径
      - **status** *(number)* - 状态码，0 为成功
      - **errMsg** *(string)* - 成功为 ok，失败为失败原因

    错误返回参数

    - **errCode** *(number)* -	错误码
    - **errMsg** *(string)* -	错误信息，格式 apiName:fail msg

  :示例-Promise:

    .. code:: js

      const cloud = require('wx-server-sdk')

      exports.main = async (event, context) => {
        const fileList = ['cloud://xxx', 'cloud://yyy']
        const result = await cloud.getTempFileURL({
          fileList,
        })
        return result.fileList
      }
