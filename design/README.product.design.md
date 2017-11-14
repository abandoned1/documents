Product - 服务器库 设计说明
说明:

设计思想:
1.业务分类（用术语完成:product_business_Catalog）默认值：硬件、网络、操作系统
 
一、系统变量

二、请求设计


四、对象设计

五、数据库设计
product_business(业务表)
 bid: 主键
 name: 名称
 catalog:(1.硬件、网络，操作系统)
 operate: 业务操作(1.只选择内容(Only select content)，2.选择内容和编辑个数(Select content and    
                  editing a number)，3.编辑个数(Editing a number)，4.硬件(Select hardware))
 entity_type: 类型类型
 created: 创建时间
 changed: 更改时间
 uid: 用户ID
 langcode: 语言

product_business_conent(业务内容-字符串)
  cid: 主键
  name:内容名称
  businessId: 所属业务
  langcode: 语言

product_business_entity_conent(业务内容－实体) 
  cid: 主键
  entity_type: 实体类型
  target_id： 实体Id
  businessId: 所属业务
  langcode: 语言

product(产品表)
  pid:主键
  server_type:所属服务器分类
  name: 名称
  description: 描述
  parameters:参数,
  custom_business: 是否可自选业务，
  max_ip: 最大IP数
  max_Port: 最大端口数
  created: 创建时间
  changed: 更改时间
  uid: 用户ID 
  langcode: 语言
+ rids: 机房 varchar(100)

product_default_business:产品默认业务表
  productId: 所属产品
  businessId: 业务ID
  business_content:业务内容

product_price(产品价格设置)
  pid: 主键
  productId:所属产品
  user_level:代理级别
  payment_mode:付款方式
  price:价格
  created: 创建时间
  changed: 更改时间
  uid: 用户ID 
  langcode: 语言

product_business_price
  bpId: 主键
  productId: 所属产品
  user_level: 代理级别
  payment_mode:付款方式
  businessId: 业务ID
  business_content:业务内容,
  price:价格
  created: 创建时间
  changed: 更改时间
  uid: 用户ID 
  langcode: 语言
