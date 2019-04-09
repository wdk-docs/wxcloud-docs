init 初始化
============

在调用云开发各 API 前，需先调用初始化方法 init 一次（全局只需一次）

init 方法的定义如下：

function init(options): void
init 方法接受一个可选的 options 参数，方法没有返回值。

options 参数定义了云开发的默认配置，该配置会作为之后调用其他所有云 API 的默认配置，options 提供的可选配置如下：

字段	数据类型	必填	默认值	说明
env	string | object	否	default	默认环境配置，传入字符串形式的环境 ID 可以指定所有服务的默认环境，传入对象可以分别指定各个服务的默认环境，见下方详细定义
当 env 传入参数为对象时，可以指定各个服务的默认环境，可选字段如下：

字段	数据类型	必填	默认值	说明
database	string	否	default	数据库 API 默认环境配置
storage	string	否	default	存储 API 默认环境配置
functions	string	否	default	云函数 API 默认环境配置
示例代码：

const cloud = require('wx-server-sdk')
cloud.init({
  env: 'test-x1dzi'
})
需要特别注意的是，在 wx-server-sdk 中不再兼容 success、fail、complete 回调，总是只会返回 Promise。