*server-room-desigin* server-room(机房管理)

说明:
1. 对机房信息进行列表展示

问题:
1. 需求问题:
	a) 机房信息列表(机房标识，机柜数量，服务器，已使用， 未使用)
	b) 机房信息编辑(机房标识，所在地区，线路类型，图片， 简介， 机房描述，机柜排列最大行数， 机柜排列最大列数， 显示顺序，前台是否可见， 网速测速网址)
	c) 机柜信息列表(服务器编号，服务器IP，交换机端口，机型， 性质， 起始时间， 终止时间)
	d) 机柜信息编辑(交换机数量, 交换机信息, 机柜入口带宽, 机柜预分配IP, 机柜最终服务商, 最终服务商信息, 机柜可放置机器最大台数)
	e) 服务器信息编辑(服务器标识， 服务器IP，服务器IP2， 交换机端口，服务器类型，服务器规格， 服务器关联订单，起始时间， 终止时间)
	f) 添加机柜数据导出功能
2. 需求问题
	a) 管理IP的分配，关联到机房->机柜->订单
	b) 一台服务器存在关联多个订单

预定义术语集
  地区
  线路类型（电信，联通，双线....)

一、 系统变量 ~

二、 请求设计 ~ 

三、 权限设计 ~

四、 对象设计 ~

五、 数据库设计 ~
rooms(机房)
!rid: 机房ID(主键)
!title(name): 机柜标识(名称) varchar(32)
count: 机柜数量 int
cid: 机柜ID(外键) int
!aid: 地区ID(通过术语ID获取)(region) int
!lid: 线路类型(通过术语ID获取)(line) int
!fid: 图片ID int
!description: 机房描述 varchar(1024)
!rows: 机柜排列最大行数 int
!cols: 机柜排列最大列数 int
!weight: 显示顺序 int
!display: 是否可见(0,1) int
!url: 机房测试地址 varchar(255)

cabinets(机柜)
cid: 机柜ID(主键) int
title: 机柜标识(名称) varchar(32)
switch_count: 交换机数量 int
switch_description: 交换机信息 varchar(255)
bindwidth: 机柜入口带宽 varchar(255)
preips:  预分配ip varchar(255)
provider: 机柜最终服务商 varchar(255)
provider_description: 机柜最终服务商描述信息 varchar(255)


六、 APIs设计 ~
