数据库导出
===============

云开发控制台支持导出集合已有的数据。目前仅支持导出 CSV、JSON 格式的文件数据。

要导出数据，需打开云开发控制台，切换到 “数据库” 标签页，并选择要导出数据的集合，点击 “导出” 链接。

.. image:: https://developers.weixin.qq.com/miniprogram/dev/wxcloud/res/guide/database/cloudconsole-database-export-dialog.jpg?t=19041015
  :alt: 数据库

选择要导出的格式、保存的位置，以及字段，点击 “导出” 按钮即可开始导出的过程。

当选择导出格式为 JSON 时，若不填写字段项，则默认导出所有数据。

当选择导出格式为 CSV 时，则字段为必填项。字段之间使用英文逗号隔开，例如：

_id,name,age,gender