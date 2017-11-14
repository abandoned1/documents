服务器－配件库 设计
目的:
1. 服务器基本配件和各类配件属性的统一管理。

说明:
1. 配件分类管理(添加，编辑，删除，列表，搜索，库存统计)
2. 配件的管理(添加，编辑，删除，列表，搜索，库存统计)

*. 设计思路:

统计列表设计思路
  配件使用列表(现有数据字段：总数，使用数)
    1.内存和硬盘容量输入方式统一(选择或输入数字)。
    2.在配件表里增加三个字段（使用－租用、使用-空闲、故障数）删除现有的使用数字段。
    ？这些值在什么地方保存进来能不参保存进来我还确定？
  
  配件采购列表（已购进）
    1.创建一张采购名细表字段（所属配件、采购数量、入库时间、入库人）

待处理问题(@todo):
  1. 配件租用在使用，配件租用空闲，配件故障等状态未设置。

一、配置变量


二、请求设计
admin/part:  首页
admin/part/list: 配件列表
admin/part/cpu/add: 增加CPU
admin/part/mainboard/add: 增加主板
admin/part/memory/add: 增加内存
admin/part/harddisc/add: 增加硬盘
admin/part/chassis/add: 增加机箱
admin/part/raid/add: 增加raid卡
+ admin/part/network/add: 增加网卡
+ admin/part/optical/add: 增加光模块
+ admin/part/switch/add: 增加交换机
admin/part/{part}/edit: 编辑配件
  admin/part/cpu/{part_cpu}/edit: 编辑CPU，由编辑配件跳转到
  admin/part/mainboard/{part_mainboard}/edit: 编辑主板，由编辑配件跳转到
  admin/part/memory/{part_memory}/edit: 编辑内存，由编辑配件跳转到
  admin/part/harddisc/{part_harddisc}/edit: 编辑硬盘，由编辑配件跳转到
  admin/part/chassis/{part_chassis}/edit: 编辑机箱，由编辑配件跳转到
  admin/part/raid/{part_raid}/edit: 编辑Raid卡，由编辑配件跳转到
  + admin/part/network/{part_network}/edit: 编辑网卡，由编辑配件跳转到
  + admin/part/optical/{part_optical}/edit: 编辑光模块，由编辑配件跳转到
  + admin/part/switch/{part_switch}/edit: 编辑交换机，由编辑配件跳转到
admin/part/{part}/delete: 删除配件

三、权限设计
administer parts list
administer parts edit
administer parts delete
administer parts add
access administration parts pages

四、实体设计
part (配件实体－基类)
  pid: （自增)作为配件主键，
  uuid: 唯一码
  type: 配件类型|CPU,主板,内存,等等
  brand: 品牌
  model: 型号
  standard: 规格
  stock: 库存数量-未使用
  stock_used: 使用库存
  ppid: 配件编号| 不同配件的编号

公用字段类：
  brand: (品牌)
  model:（型号）
  standard: （规格）
  langcode:  语言
  stock: 库存
  created: int(11) 创建时间
  changed: int(11) 更改时间
  uid: int(11) 用户ID
  ＋ description: 描述

part_cpu(cpu实体－继承公用字段类)
  cid: ID(主键）
  suitable: varchar(32) 适用类型
  family: varchar(32) 系列
  frequency: varchar(16) 主频
  max_frequency: varchar(16) 最大睿频
  out_frequency: varchar(16) 外频
  slot_type: varchar(128) 插槽类型
  kernel_code: varchar(128) 核心代号
  kernel_num:  varchar(128) 核心数量
  thread_num: varchar(128) 线程数
  cache_level_1: varchar(128) 一级缓存
  cache_level_2: varchar(128) 二级缓存
  cache_level_3: varchar(128) 三级缓存
  memory_controller: varchar(256) 内存控制器
  processor_64bit: bool 是否64位处理器

part_mainboard(主板实体－继承公用字段类)
  mid: 主板主键
  chipmaker（芯片厂商）
  chipset（芯片组）
  chipset_description（芯片组描述）
  chipset_display（显示芯片组）
  chipset_audio(音频芯片)
  chipset_network(网卡芯片)
  cpu_platform(CUP平台)
  cpu_type(CUP类型)
  cpu_slot(CUP插槽)
  cpu_description(CUP描述)
  memory_type(内存类型)
  memory_slot(内存插槽)
  memory_max(最大内存)
  memory_description(内存描述)  
  pcie_slot(PCI-E插槽)
  pci_slot(PCI插槽)
  sata_interface(sata接口)
  usb_interface(usb接口)
  hdmi_interface(HDMI接口)
  outer_port(外接端口)
  ps2_interface(ps/2接口)
  other_interface(其它接口)
  mainboard_type(板型)
  system_not(不支持系统)
  + support_ipmi (是否支持ipmi接口)

part_memory(内存实体－继承公用字段类)
  mid: 内存主键
  suitable               taxonomy_term_reference   //适用类型
	capacity		           taxonomy_term_referende   //内存容量
	capacity_description	 varchar(50)		           //容量描述
	memory_type		         taxonomy_term_reference   //内存类型
	memory_clocked			   taxonomy_term_referende   //内存主频
	practicle_config       taxonomy_term_reference   //颗粒配置
  cl_delay               int                       //CL延迟
  production_process     taxonomy_term_reference   //制作工艺

part_harddisc(硬盘实体－继承公用字段类)
  hid: 硬盘主件
  suitable            varchar(15)  //适用类型
  size                varchar(15)  //尺寸
  hard_disc_capacity  int          //磁盘容量
  discs_number        int          //盘片数量
  per_disc_capacity   int          //单碟容量
  head_number         int          //磁头数量
  cache               int          //缓存(单位：MB)
  speed               int          //转速(单位：rpm)
  interface_type      varchar(20)  //接口类型
  interface_speed     int          //接口速率(单位：GB/秒)
  + harddisk_type         int          //硬盘类型（HDD,SSD）

part_chassis(机箱－继承公用字段类)
  cid: 机箱主键
  disk_number: (硬盘位)
  + support_raid: Raid卡是否⽀支持

part_raid(raid卡－继承公用字段类)
  cid: raid卡主建

+part_network(网卡－继承公用字段类)
  nid: 网卡主建

+part_optical(光模块－继承公用字段类)
  oid: 光模块主建

+part_switch(交换机－继承公用字段类)
  sid: 交换机主建
  port_number: 端口数

五、数据库设计

六、APIs设计

