服务器－机房  设计
目的:
1. 对机房相关信息的管理

说明:
1. 机房列表管理（机房编号，机房名称，地区）
2. 机房编辑(机房名称，机房所在地区，线路类型，图片，简介，机房描述，显示顺序，前台是否可见，网速测试地址)
3. 机房查看(显示机房各机柜图形(机柜编号，服务器总量，未使用量，已使用量，交换机数，故障数)
4. 机柜上的服务器列表(所在机柜号，所在机房，机位，交换机列表、端口(一、二）信息，
   图形表示机柜机位所占服务器详情（机位，服务器编号，管理IP，交换机，交换机端口，机型，状态（使用与否))
5. 服务器基础数据及使用详情(硬件配置基础，附加配件，附加业务，服务器流水）

模块名：
 IDC Room

设计思路：
1.创建机房的内容实体
2.创建机柜的内容实体
3.为机房增加机柜。
 
二、请求设计
 admin/idc/room: 机房列表
 admin/idc/room/add: 增加机房
 admin/idc/room/{room}/edit: 编辑机房
 admin/idc/room/{room}/delete: 删除机房
 admin/idc/room/{room}/cabinet： 机房机柜列表
 admin/idc/cabine/add: 增加机柜
 admin/idc/cabinet/{room_cabinet}/edit:编辑机柜
 admin/idc/cabinet/{room_cabinet}/delete: 删除机柜
 admin/idc/cabinet/{room_cabinet}/seat： 机柜机位服务器列表
 admin/idc/cabinet/{room_cabinet}/seat/{seat}/server/add: 增加服务器
 admin/idc/cabinet/{room_cabinet}/seat/{seat}/switch/add: 增加交换机
 admin/idc/server/seat/{cabinet_server}/delete: 删除此机位上的服务器
 admin/idc/switch/seat{cabinet_switch}/delete： 删除些机位上的交换机
 
三、权限设计
 administer idc room view
 administer idc room edit
 administer idc room delete

三、实体设计
 idc_room（IDC 机房）
   rid: 主键
   name: 机房名称
   area: 所在地区（术语）
   circuit： 线路类型（术语）
   image: 图片
   introduction：简价
   description：描述
   front_visible:前台可见（术语）
   speed_test_address:网速测试地址
   cabinet_number: 机柜数。
   created: 创建时间
   changed: 更改时间
   uid: 用户ID
   
 idc_room_cabinet(机房机柜)
   cid: 主键
   rid： 所属机房
   code: 机柜编号
   seat：机位数
   used_seat: 已使用机位
   unused_seat: 未使用机位
   switch_seat: 交换机数
   fault_seat: 故障数
   created: 创建时间
   changed: 更改时间
   uid: 用户ID 

 idc_cabinet_server(服务器与机柜关联)
  sid:主键Id
  ipm_id: 管理IP的id（从IP库里选择）
  cabinet_id: 所属机柜
  start_seat:起始机位
  seat_size: 机型占几u
  switch_p_target_id:交换机P （选择增加到机柜上的交换机）
  switch_p_value:交换机IP端口
  switch_m_target_id: 交换机M  (选择增加到机柜上的交换机）
  switch_m_value :交换机M端口
  server_id: 所属服务器 (选择服务器库里的服务器)
  created: 创建时间
  changed: 更改时间
  uid: 用户ID
  +group_name: 保存刀片机的组名
  +parent_id: 所属父id

idc_cabinet_switch (交换机与机柜关联）
  sid: 主键Id
  cabinet_id: 所属机柜
  start_seat:起始机位
  seat_size: 机型占几U
  ips_id: 交换机IP的id(从IP库里选择IP)
  created: 创建时间
  changed: 更改时间
  uid: 用户ID

