日志模块的功能设计:

目的:
  1. 统一管理Hostspace业务的日志系统。

设计思想:
1. 使用系统日志模块，各个模块再进入增加

一、系统变量

二、请求设计
  /admin/log/list: 日志列表
  admin/log/{log_id}/view： 日志详情
三、权限设计
  access administration log pages: Hostspace查看

五、数据库设计
operation_log(操作日志)
  lid: 主键
  uid: 操作用户
  timestamp: 操作时间
  action: 动作
  message: 信息
  entity_id： 操作对象id,
  entity_name：操作对象名称（实体名或表名）
  data_id： 对象相关联表操作的id
  data_name: 对象相关联表的表名
  data: 数据(BLOB类型)
  
各个模块的调用方法如：
 HostLogFactory::OperationLog('ip')->log($clone_entity, 'insert');
 HostLogFactory::OperationLog('ip')->log($entity, 'update');
 HostLogFactory::OperationLog('ip')->log($this->entity, 'delete');


建意不要xunyunlog表存的日志了，因为我觉得operation_log表的日志包含了xunyunlog表的日志。




