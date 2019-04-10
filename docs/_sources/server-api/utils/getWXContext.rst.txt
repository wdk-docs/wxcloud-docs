:wxcloud:`getWXContext <reference-server-api/utils/getWXContext>`
======================================================================

.. js:function:: cloud.getWXContext()

   在云函数中获取微信调用上下文

   :returns:

    - **OPENID**	小程序用户 openid	(小程序端调用云函数时)
    - **APPID**	小程序 AppID	(小程序端调用云函数时)
    - **UNIONID**	小程序用户 unionid	(小程序端调用云函数，并且满足 unionid 获取条件时)
   :示例:

    .. code:: js

      const cloud = require('wx-server-sdk')

      exports.main = async (event, context) => {
        const {OPENID, APPID, UNIONID} = cloud.getWXContext()
        return {OPENID, APPID, UNIONID}
      }
