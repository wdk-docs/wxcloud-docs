:wxcloud:`callFunction <reference-server-api/functions/callFunction>`
=============================================================================

.. js:function:: cloud.callFunction({name, data})

  调用云函数

  :param string name: 云函数名
  :param object data: 传递给云函数的参数
  :return: Promise返回结果说明

    - **errMsg** *(string)* - 通用返回结果
    - **result** *(string)* - 云函数返回的结果
    - **requestID** *(string)* - 云函数执行 ID，可用于在控制台查找日志	0.0.12

    错误返回参数

    - **errCode** *(number)* -	错误码
    - **errMsg** *(string)* -	错误信息，格式 apiName:fail msg

  :示例函数:

    .. code:: js

      exports.add = (event, context, cb) => event.x + event.y

  :示例代码:

    .. code:: js

      const cloud = require('wx-server-sdk')
      exports.main = async (event, context) => {
        const res = await cloud.callFunction({
          // 要调用的云函数名称
          name: 'add',
          // 传递给云函数的参数
          data: {
            x: 1,
            y: 2,
          }
        })
        return res.result
      }
