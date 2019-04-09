数据库 API
=============

小程序·云开发提供了丰富的数据库操作 API，此处是数据库 Server 端的 API 参考文档，可用于云函数运行环境。

Server 端的 API 与小程序端基本保持一致，有如下不同：

Server API 不再接受回调（success, fail, complete），统一返回 Promise
Server 端有批量写和批量删除的权限，即可在集合或查询语句上调用 update 或 remove
Server 端独有 API 如创建集合（db.createCollection）
数据库 API 都是懒执行的，这意味着只有真实需要网络请求的 API 调用才会发起网络请求，其余如获取数据库、集合、记录的引用、在集合上构造查询条件等都是不会触发网络请求的。触发网络请求的 API 有如下几个：

API	说明
get	获取集合 / 记录数据
add	在集合上新增记录
update	更新集合 / 记录数据
set	替换更新一个记录
remove	删除记录
count	统计查询语句对应的记录条数
获取引用的 API 有如下几个：

API	说明
database	获取数据库引用，返回 Database 对象
collection	获取集合引用，返回 Collection 对象
doc	获取对一个记录的引用，返回 Document 对象
在数据库 (Database) 对象上有如下字段：

字段	说明
command	获取数据库查询及更新指令，返回 Command
serverDate	构造服务端时间
Geo	获取地理位置操作对象，返回 Geo 对象
createCollection	创建一个集合
在集合 (Collection) 对象上有如下 API：

API	说明
doc	获取对一个记录的引用，返回 Document 对象
add	在集合上新增记录
update	更新数据
where	构建一个在当前集合上的查询条件，返回 Query，查询条件中可使用查询指令
remove	删除匹配相应筛选条件的记录
orderBy	指定查询数据的排序方式
limit	指定返回数据的数量上限
skip	指定查询时从命中的记录列表中的第几项之后开始返回
field	指定返回结果中每条记录应包含的字段
在记录 (Document) 对象上有如下 API：

API	说明
get	获取记录数据
update	局部更新数据
set	替换更新记录
remove	删除记录
field	指定返回结果中记录应包含的字段
Command (db.command) 对象上有如下查询指令：

API	说明
eq	字段是否等于指定值
neq	字段是否不等于指定值
lt	字段是否小于指定值
lte	字段是否小于或等于指定值
gt	字段是否大于指定值
gte	字段是否大于或等于指定值
in	字段值是否在指定数组中
nin	字段值是否不在指定数组中
and	条件与，表示需同时满足另一个条件
or	条件或，表示如果满足另一个条件也匹配
Command (db.command) 对象上有如下更新指令：

API	说明
set	设置字段为指定值
remove	删除字段
inc	原子自增字段值
mul	原子自乘字段值
push	如字段值为数组，往数组尾部增加指定值
pop	如字段值为数组，从数组尾部删除一个元素
shift	如字段值为数组，从数组头部删除一个元素
unshift	如字段值为数组，往数组头部增加指定值
API reject 时返回的 Error 对象均含以下两个字段：

字段	类型	说明
errCode	number	错误码
errMsg	string	错误信息