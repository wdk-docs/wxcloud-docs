测试、日志与监控
=================

测试
--------

云开发提供了云函数测试功能，可以方便地调试你的代码。在控制台的对应云函数的管理面板中，点击 “测试” 按钮即可打开测试弹窗。

.. image:: https://developers.weixin.qq.com/miniprogram/dev/wxcloud/res/functions/function_test.png?t=19041015

测试弹窗
----------

点击“提交方法”下拉菜单可以选择测试函数的模板方法，当前只支持Hello World 事件模板。模板在测试时作为 event 参数传递给函数。在“测试参数”的编辑器中输入想测试的参数后，点击“执行”按钮即可运行代码。执行完毕后将在“运行测试”栏显示运行结果。

除了可视化的云函数测试功能，我们还提供命令行工具 scf-cli, 助你在本地快速调试。

日志
--------

在这里可以查看云函数的调用日志，方便开发者对开发调试。

.. image:: https://developers.weixin.qq.com/miniprogram/dev/wxcloud/res/functions/function_log.png?t=19041015

监控
------

在这里可以查看云函数的调用次数、运行时间、错误次数。并支持将这些数据导出。

.. image:: https://developers.weixin.qq.com/miniprogram/dev/wxcloud/res/functions/function_monitor.png?t=19041015