wx.cloud.callFunction
=====================

调用云函数

OBJECT参数说明

参数	类型	必填	说明
name	String	是	云函数名
data	Object	否	传递给云函数的参数
config	Object	否	局部覆写 wx.cloud.init 中定义的全局配置
success	Function	否	返回云函数调用的返回结果
fail	Function	否	接口调用失败的回调函数
complete	Function	否	接口调用结束的回调函数（调用成功、失败都会执行）