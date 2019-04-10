:wxcloud:`callFunction <reference-client-api/functions/callFunction>`
=============================================================================

.. js:function:: wx.cloud.callFunction({name[, data][, config][, success][, complete][, success]})

   调用云函数

   :param string name: 云函数名
   :param object data: 传递给云函数的参数
   :param object config: 局部覆写 wx.cloud.init 中定义的全局配置
   :param function success(errMsg, result, requestID): 返回云函数调用的返回结果

     - **errMsg** *(string)* - 通用返回结果
     - **result** *(string)* - 云函数返回的结果
     - **requestID** *(string)* - 云函数执行 ID，可用于在控制台查找日志	2.3.0

   :param function fail(errCode, errMsg): 接口调用失败的回调函数

     - **errCode** *(number)* -	错误码
     - **errMsg** *(string)* -	错误信息，格式 apiName:fail msg

   :param function complete: 接口调用结束的回调函数（调用成功、失败都会执行）
   :例(函数):

    .. code:: js

      exports.add = (event, context, cb) => event.x + event.y

   :例(Callback):

    .. code:: js

      wx.cloud.callFunction({
        // 要调用的云函数名称
        name: 'add',
        // 传递给云函数的参数
        data: {
          x: 1,
          y: 2,
        },
        success: res => {
          // output: res.result === 3
        },
        fail: err => {
          // handle error
        },
        complete: () => {
          // ...
        }
      })

   :例(Promise):

    .. code:: js

      wx.cloud.callFunction({
        // 要调用的云函数名称
        name: 'add',
        // 传递给云函数的event参数
        data: {
          x: 1,
          y: 2,
        }
      }).then(res => {
        // output: res.result === 3
      }).catch(err => {
        // handle error
      })
