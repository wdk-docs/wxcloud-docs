:wxcloud:`初始化 <reference-client-api/init>`
==================================================


.. js:function:: wx.cloud.init([ {[ {env : [{[ database ][ , storage ][ ,functions ]} || 'string'] ][ ,traceUser ]} ])

   在调用云开发各 API 前，需先调用初始化方法 init 一次（全局只需一次）

   :param env: 默认环境配置，传入字符串形式的环境 ID 可以指定所有服务的默认环境，传入对象可以分别指定各个服务的默认环境，见下方详细定义
   :type env: string | object
   :param string database: 数据库 API 默认环境配置 默认值 default
   :param string storage: 存储 API 默认环境配置 默认值 default
   :param string functions: 云函数 API 默认环境配置 默认值 default
   :param boolean traceUser: 是否在将用户访问记录到用户管理中，在控制台中可见 默认值 false
   :示例:

     .. code:: js

      wx.cloud.init({
        env: 'test-x1dzi'
      })

