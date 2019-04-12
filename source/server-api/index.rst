服务端 API
=======================

云端运行环境为 Node.js，开发时请安装 Node.js 和 npm。

使用云开发需在云函数目录中安装 wx-server-sdk 依赖：

.. code-block:: sh

  npm install --save wx-server-sdk

在工具云函数根目录中创建云函数时，默认会创建一个定义了 wx-server-sdk 依赖的 package.json，
并在创建成功时提示自动安装依赖。如果在你的环境中无法直接使用 npm install，
比如需要走代理、使用自建的 npm 源站、使用其他包管理器如 yarn 等的情况，则不能使用工具的自动安装依赖，需手工执行相应依赖安装命令。

需要特别注意的是，在 wx-server-sdk 中不再兼容 success、fail、complete 回调，总是只会返回 Promise。

以下是 wx-server-sdk API 文档分类入口：

.. toctree::
   :maxdepth: 4
   :glob:

   init
   utils/index
   database/index
   storage/index
   functions/index
