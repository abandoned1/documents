###支付方式
####目的:
- 整合网站支付方式
####说明:
  - 后台支付方式管理
  - 前台订单支付
####设计思路
####系统变量
####请求设计
> 后台
  admin/config/payment/methods: 支付方式管理列表
  admin/config/payment/add: 支付方式添加
> 前台

####权限设计
####对象设计
####数据库设计
payment:
  pid: 序号
  ppid: 支付方式的ID
  type: 类型
  name:
  code:
  description:
  enabled:
  weight:
alipay:
  pid: 序号
  account: 支付宝账号
  verifycode: 安全较验码
  partnerid: 合作者身份ID
  type: 支付宝类型

  code: 支付方式的编码 string(15)
  name: 支付方式名称string(56)
  description: 支付方式描述 string(255)
  fee: text
  config: text_long
  cod: boolean
  config: boolean
  cod: boolean
  online: boolean 在线，线下
  weight: integer
  enabled: boolean 启用，未启用
  return_url: string (156)
  notify_url: string (156)


Yeepay:(易宝)
  pid: 序号
  code: 商户编号
  key: 商户密钥

  code: 支付方式的编码 string(15)
  name: 支付方式名称string(56)
  description: 支付方式描述 string(255)
  fee: text
  config: boolean
  cod: boolean
  online: boolean 在线，线下
  weight: integer
  enabled: boolean 启用，未启用
