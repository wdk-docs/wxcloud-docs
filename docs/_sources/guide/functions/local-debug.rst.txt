云函数本地调试功能
==================

云开发提供了云函数本地调试功能，方便开发者在本地进行云函数调试。

使用须知
----------

若云函数中有使用使用到 npm 模块，需在云函数本地目录安装相应依赖才可正常使用云函数本地调试功能。
系统默认使用开发者工具自带的 Node.js，用户可通过点击本地调试的设置进行修改。

.. image:: https://developers.weixin.qq.com/miniprogram/dev/wxcloud/res/functions/local_debug_settings.png?t=19041015
   :alt: 描述

运行环境要求
下载并安装 1.02.1903211 或以上版本的开发者工具，下载地址。
使用流程

1. 打开本地调试界面

开发者可通过右键点击云函数名唤起本地调试界面。

.. image:: https://developers.weixin.qq.com/miniprogram/dev/wxcloud/res/functions/local_debug_entry.png?t=19041015
   :alt: 描述

在本地调试界面中点击相应云函数并勾选【开启本地调试】方可进行该云函数的本地调试。 在开启本地调试的过程中，系统会检测该云函数本地是否已安装了 package.json 中所指定的依赖，如无会给出警告。 对于已开启本地调试的云函数，微信开发者工具模拟器中的对该云函数的请求、以及其他开启了本地调试的云函数的对该云函数的请求，都会自动请求到该本地云函数。

.. image:: https://developers.weixin.qq.com/miniprogram/dev/wxcloud/res/functions/local_debug_enable.png?t=19041015
   :alt: 描述

3. 调试方式

目前云函数本地调试的请求方式支持：

手动触发：在本地调试界面输入请求参数并发起调用。
模拟器触发：直接在IDE模拟器发起对该云函数的请求。
在手动触发的模式下，系统支持两种模拟方式：

从小程序端调用：在云函数内可通过 cloud.getWXContext() 获取调用的微信上下文，包括 OPENID 等字段。
从其他云函数调用：调用时云函数内不带有微信上下文。

4. 模板管理

在手动触发的条件下，开发者需手动输入请求参数。为方便开发者进行模板管理，系统提供了模板的保存、另存为及删除功能。

同时在云函数本地调试界面保存模板时，系统会在小程序本地代码目录下创建cloudfunctionTemplate目录，并新建该云函数的模板文件。开发者也可通过直接修改该模板文件进行模板的管理。

.. image:: https://developers.weixin.qq.com/miniprogram/dev/wxcloud/res/functions/local_debug_template.png?t=19041015
   :alt: 描述