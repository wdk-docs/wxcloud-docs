:wxcloud:`上传 <reference-server-api/storage/uploadFile>`
=============================================================================

.. js:function:: cloud.uploadFile({cloudPath, fileContent})

  将本地资源上传至云存储空间，如果上传至同一路径则是覆盖写

  :param string cloudPath: 云存储路径
  :param fileContent: 要上传文件的内容
  :type fileContent: Buffer 或 fs.ReadStream
  :rtype: Promise<result>
  :return:

    Promise返回结果说明

    - **fileID** *(String)* -	文件 ID
    - **statusCode** *(Number)* -	服务器返回的 HTTP 状态码

    错误返回参数

    - **errCode** *(Number)* -	错误码
    - **errMsg** *(String)* -	错误信息，格式 apiName:fail msg

  :示例-Promise:

    .. code:: js

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
