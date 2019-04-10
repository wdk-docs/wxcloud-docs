:wxcloud:`下载 <reference-server-api/storage/downloadFile>`
===============================================================================

.. js:function:: cloud.downloadFile({fileID})

  从云存储空间下载文件

  :param string fileID: 云文件 ID
  :rtype: downloadTask
  :return:

    Promise返回结果说明

    - **fileContent** *(Buffer)* -	文件内容
    - **statusCode** *(Number)* -	服务器返回的 HTTP 状态码

    错误返回参数

    - **errCode** *(Number)* -	错误码
    - **errMsg** *(String)* -	错误信息，格式 apiName:fail msg

  :示例-Promise:

    .. code:: js

      const cloud = require('wx-server-sdk')

      exports.main = async (event, context) => {
        const fileID = 'xxxx'
        const res = await cloud.downloadFile({
          fileID,
        })
        const buffer = res.fileContent
        return buffer.toString('utf8')
      }
