Server - 服务器库 设计说明
说明:
  1. 定义网站服务器产品名称.
  2. 定义服务器组装及其具体配置.

设计思想:
  1. 将服务器产品名称定义为术语.
  2. 用内容实体保存服务器具体配置.

一、系统变量

二、请求设计
admin/server: 服务器列表
admin/server/{server}/part: 服务器配件
admin/server/{server}/part/detail: 服务器详情
admin/server/package: 服务器组装
admin/server/host: 服务器主机列表(术语列表) -- 可能不会需要额外的添加和编辑页面.

三、权限设计
administor server view: 服务器浏览
administor server edit: 服务器编辑(组装)
administor server delete: 服务器删除

四、对象设计

五、数据库设计
设置服务器表自增: alter table users AUTO_INCREMENT=10000;
db_query("SELECT * FROM {watchdog} WHERE wid = :wid", array(':wid' => $id))
        ->fetchAssoc();
 

服务器库(server):
  sid: 服务器序号
  server_code: 服务器编号
  type: 类型|配置一、配置二、配置三(用术语)
  name: 服务器名称|服务器配置描述
//  status: 服务器使用状态| 在用(Used)、未用(Unuse),保留(Keep)，故障(fault) (用术语) | server_used_type
  status_equipment: 服务器上架状态| 已上柜(on)、待上柜(off)
  uid: 创建用户
  created: 创建时间
  modified: 修改时间
//  server_type: 服务器类型｜租用(hire)，托管(deposit)  //术语列表 | server_rent_type
+ additional: 额外配件
+ rid: 机房 varchar
