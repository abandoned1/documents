HOSTSPACE 网站日志系统

所有日志的公共字段
  op_date : 操作时间
  op_user : 操作人
  op_ip : 操作的IP地址

// 服务器使用流水记录。。。。。。？？？？？？？？？
服务器的使用日志：
server_log
  hid : int 日志编号  自增主键 [服务器在线编码 dc_hostclient 表中的hid字段]
  m_ip: varchar 服务器IP  
  server_id : 服务器编码
  client : int 想关客户编号
  start_stmap : 服务开始时间戳
  end_stamp : 服务结束时间戳  

服务器流水 显示指定机器的业务变更流水
  //一条记录表示某台机器在某个客户使用的情况下所产生的业务变更记录
  server_business_change_log 服务器业务变更记录
    id : 日志主键
    hid : 使用记录。【在某个客户的服务期限中】
    business : 服务器对应的业务 [硬件业务（内存 硬盘）网络业务(IP 带宽 高防) ]
    op_type : 业务的变更类型 (新增/下架)
    op_date : 时间
    op_user : 操作用户
    op_ip : 操作的IP地址
//---------------------------------。

用户登录日志：
user_login_log
  id : int 日志编号 自增主键
  login_ip : varchar 登录的IP地址
  user : int 用户编号
  login_date : int 登录时间
  out_date : int 登出时间

网站访问日志：
web_access_lpg
  id : int 日志编号 自增主键
  access_ip : varchar 访问的IP地址
  user : int 用户编号
  access_url : varchar 访问路径
  access_date : int 访问时间

机房操作日志
room_log
  id : 日志主键
  room_id : 机房编码
  op : 操作内容 (添加机房 /添加机柜 /删除机柜 )
  op_user : 操作用户
  op_date : 操作日期
  op_ip : 操作的IP地址

机柜操作日志
cabinet_log
  id : 日志主键
  cabinet_id : 机柜号
  seat_id : 机位号 
  op : 操作内容 (对机位而言：绑定服务器(交换机)到机位 /将服务器从机位移除) (对机柜：修改机柜信息)
  op_user : 操作用户
  op_ip :  操作的IP地址
  op_date : 操作日期

配件库操作日志
part_library_log
  id :
  type : varchar 配件类型 [内存 硬盘 CPU 主板 机箱]
  op : 操作内容 (机房新入库 /修改信息 /删除配件)
  op_date : 操作时间
  op_user : 操作人
 ？？ op_num : 操作数量

IP库操作日志
ip_library_log
  id : 日志主键
  type : ip类型[交换机ip 业务ip  管理ip]
  op : 操作内容 (机房新入库IP /修改IP信息 /删除IP)
  op_date : 操作时间
  op_user : 操作人

???
务器的更新日志
idc_hostclient_log
  id : 日志主键编号
  hid : 对应的服务器数据编号 （服务器入库之后，hid对应的记录删除！） 
  server_id : 服务器编号
  op_type : 服务器更新类型 (上架/下架业务ip 新增/下架高防 添加内存/硬盘 ......)
  op_business : 操作的业务
  op_date : 操作时间
  op_user : 操作人
???

用户变更日志
user_change_log
 id : 日志编号
 uid : 用户编号
 op_type : 添加/注册/信息修改
 op_content : 操作内容
 op_date : 操作时间
 op_user : 操作人 

  
产品操作日志
product_log
  id : 日志编号
  product : 对应的产品
  op_type : 操作类型 （添加产品  修改产品信息  产品价格设置 产品自选业务价格设置）
  op_content : 操作内容
  op_date : 操作时间
  op_user : 操作人
  
附加业务的操作日志
business_log
  id : 日志编号
  business : 对应的业务
  op_type : 操作类型
  op_content : 操作内容
  op_date : 操作时间
  op_user : 操作人

