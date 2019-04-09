云调用
========

版本要求：wx-server-sdk >= 0.4.0、开发者工具 >= 1.02.1903251 （目前需开发版或测试版）

云调用是云开发提供的基于云函数使用小程序开放接口的能力。云调用需要在云函数中通过 wx-server-sdk 使用。在云函数中使用云调用调用服务端接口无需换取 access_token，只要是在从小程序端触发的云函数中发起的云调用都经过微信自动鉴权，可以在登记权限后直接调用如发送模板消息等开放接口。

使用方法
1. 查看服务端接口是否支持云调用
在服务端接口列表中罗列了所有的服务端接口，如果接口支持云调用，则在接口名称旁会带有 云调用 的标签。同时，在每一个服务端接口文档中，如果接口支持云调用，也会有专门的支持说明以及相应的使用文档。

2. 查看接口的云调用文档
在支持云调用的接口文档中，会分别列出 HTTPS 调用的文档及云调用的文档，云调用文档同 HTTPS 调用文档一样包含请求参数、返回值及示例。


3. 为云函数声明所需调用的接口
接着，需要配置云调用权限，每个云函数需要声明其会使用到的接口，否则无法调用，声明的方法是在云函数目录下的 config.json（如无需新建）配置文件的 permissions.openapi 字段中增加要调用的接口名，permissions.openapi 是个字符串数组字段，值必须为所需调用的服务端接口名称。在每次使用微信开发者工具上传云函数时均会根据配置更新权限。以下是一个示例的声明了使用发送模板消息接口的配置文件：

.. code-block::

  {
    "permissions": {
      "openapi": ["templateMessage.send"]
    }
  }

4. 在云函数中使用云调用
首先云函数中需要使用版本号至少 0.4.0 的 wx-server-sdk，建议 wx-server-sdk 始终保持最新，保证云函数目录下的 package.json 的 wx-server-sdk 字段为 latest，如本地安装依赖，请执行 npm install --save wx-server-sdk@latest。

接下来，可在云函数中使用云调用 API 了。云调用 API 均挂载在 wx-server-sdk 模块的 openapi 对象下，各个开放接口类别在 openapi 对象下设二级命名空间对象（如模板消息接口的方法均在 openapi.templateMessage 下），该对象下挂载该类别下的所有开放方法（比如模板消息的发送接口是 openapi.templateMessage.send）。各接口从属的类别名称和方法名称可以通过接口名称查看，接口名称均以 <类别>.<方法> 命名，如发送模板消息的接口名称是 templateMessage.send。下面是一个给自己发送模板消息的示例：

如需可直接运行的示例，请在 IDE 中创建一个云开发快速启动模板的项目，其中有包含发送模板消息的云调用的示例

.. code-block::

  const cloud = require('wx-server-sdk')
  cloud.init()
  exports.main = async (event, context) => {
    try {
      const result = await cloud.openapi.templateMessage.send({
        touser: cloud.getWXContext().OPENID, // 通过 getWXContext 获取 OPENID
        page: 'index',
        data: {
          keyword1: {
            value: '339208499'
          },
          keyword2: {
            value: '2015年01月05日 12:30'
          },
          keyword3: {
            value: '腾讯微信总部'
          },
          keyword4: {
            value: '广州市海珠区新港中路397号'
          }
        },
        templateId: 'TEMPLATE_ID',
        formId: 'FORMID',
        emphasisKeyword: 'keyword1.DATA'
      })
      // result 结构
      // { errCode: 0, errMsg: 'openapi.templateMessage.send:ok' }
      return result
    } catch (err) {
      // 错误处理
      // err.errCode !== 0
      throw err
    }
  }