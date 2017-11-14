IP库 -业务IP  设计
目的:
1. 保存所有的业务IP信息数据

设计思想:
1. yml文件配置定义好IP相关的所有基础属性
2. 用内容实体来保存记录业务IP属性信息以及修改记录等。

一、系统变量

二、请求设计
admin/ip/list   列表
admin/ip/add    添加
admin/ip/edit   编辑
三、权限设计
administer ip view
administer ip edit
administer ip delete

四、对象设计

五、数据库设计

  管理IP字段描述:
  	id:
  	ip:
  	puid: 用户（若该字段为空则表示该IP为公用IP）
+  	status: IP使用状态在用(Used)、未用(Unuse),保留(Keep)，故障(fault) , 停用(Disabled) (用术语) | server_used_type
   	server_type: 服务器类型｜租用(hire)，托管(deposit)  //术语列表 | server_rent_type
+   status_equipment: 上架状态(on,off)
  	description: 描述
    created: 创建时间
  	changed: 更改时间
  	uid: 用户ID
+port 管理IP的端口号


  交换机:
  	id:
  	ip:
  	port: 端口总数
	  description: 描述
    created: 创建时间
  	changed: 更改时间
+   status_equipment: 上架状态(on,off)
  	uid: 用户ID

  业务IP:
  	id:
  	ip:
		puid: 业务IP专用用户
		uid: 用户ID
		status: IP使用状态在用(Used)、未用(Unuse),保留(Keep)，故障(fault) (用术语) | server_bussiness_used_type
  	type: 类型｜公共IP段、20G高防、40G高防、大带宽、ATOM专用、高防DNS、公司保留(用术语)
		ip_segment: IP段
  	description: 备注
    created: 创建时间
  	changed: 更改时间
+   status_equipment: 上架状态(on,off)
+   rid: 机房ID varchar


