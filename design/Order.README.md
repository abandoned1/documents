###订单 设计
####目的:
- 整合网站订单流程

####说明:
- 后台订单管理
- 前台订单生成
####设计思路
 1. sudo 用户 --- 代替用户下单 使用用户ID下单
####系统变量
####请求设计
> #####后台
	admin/orders/unpay: 未付款订单列表
	admin/orders/unpay/{order}/details: 订单详情
	admin/orders/unchange: 待改价订单
	admin/orders/change/{order}/detail: 待改价订单详情
	admin/orders/trial: 试用列表
	admin/orders/trial/{order}/detail: 试用订单详情
	admin/orders/trial/{orders}/expired: 试用订单到期详情
	admin/orders/list: 所有订单(完成订单)
	admin/orders/{order}/detail: 订单详情(完成订单)
-----------
> #####前台
	用户管理中心
	订单:
	user/order/list: 用户所有订单
	user/order/{status}/list: 用户{订单状态}列表
	user/order/{orderid}/detail: 订单详情
	user/order/{orderid}/cancel: 订单取消(关闭)
	user/order/{orderid}/exchange: 订单支付
	user/order/{orderid}/finish: 订单完成
	user/order/{orderid}/complete: 订单支付成功,并分配服务器相关IP.
-----------
>	前端路径架构
	server: 服务器产品列表
	server/{productid}/order: 服务器产品订购页面
	user/cart: 用户购物车
	user/checkout: 用户购物车结算
	user/checkout/order: 结算并生成订单

####权限设计
> 以下几个路径默认设为TRUE

	server: 服务器产品列表
	server/{productid}/order: 服务器产品订购页面
> 以下几个默认为登录用户

	user/cart: 用户购物车
	user/checkout: 用户购物车结算
	user/checkout/order: 结算并生成订单

>
####对象设计
	null
####数据库设计
------------
  cart: 购物车
   cid:  自增ID
   action: 行为类型：1租用2续费3升级
   product_id: 所属产品
   product_num: 数量
   product_limit: 期限
   base_price: 基本价格
   custom_price: 自定义价格
   description: 备注
   uid: 用户
   created: 机房编号
   rid: 机房编号 

  cart_business_data:
    cbid: 自增id
    business_id: 所选业务的ID，
    business_content: 所选业务的值，
    business_price: 业务的价格
    business_default: 是否默认业务，1是0不是
    cartId: 所属购物车id

	idc_order: 订单表
		oid:自增ID
		code: 订单编号
		order_price: 订单价格
		paid_price: 实收价格
		discount_price: 优惠价格
		change_price_status:改价状态(int[未申请改价， 改价审核，审核通过，审核没通过])
		trial_status: 试用状态(int[未申请试用，试用审核，审核通过，审核没通过，试用结束])
		status:状态(int[关闭，未付款，改价中，试用中，已付款])
    payment_mode: 支付方式（线下支付，支付宝）
    payment_date: 支付时间
		uid: 客户
		alias_order: 订单别名
		client_service:客服ID
    accept: 是否接受| 已经分配订单为1， 未分配订单为空
		create: 创建时间

	order_product:服务器产品
		opid:产品自增ID,
    action: 产品类型：1租用，2续费，3升级
		proeuct_id: 产品Id,
    product_name: 产品名称
    product_type: 配置分类ID(int)
		product_num: 产品数量
    product_limit: 期限(月) 
    base_price: 基本价格，
    custom_price: 自选价格
    description: 备注
    order_id: 订单自增号

  order_product_detail: 客户订单配置详情
    opdid:产品自增ID
    business_id: 业务Id
    business_name: 业务名称
    business_content: 所填业务值
    business_content_name: 业务值对应该的文本
    business_price: 是否价格
    business_default: 是否默认
    combine_mode: 与默认业务合并方式
    order_product_id: 所属订单产品Id

  order_change_price: 订单改价
		id:　自增号
		order_id: 改价订单号
    order_code: 订单编码
    client_id: 客户Id
		order_price: 订单金额
		change_price:   优惠的价格
		ask_uid: 改价申请UID
		create: 申请时间
		audit_stamp: 审核时间
		audit_uid: 审核用户ID
    description:改价描述   
    status : 状态 1待审核 2通过 3未通过
    addit_remark : 审核描述 

   order_server_trial:
     id: 自增号
     order_id: 订单Id
     client_id: 客户id,
     product_id: 产品表id,
     order_product_id: 订单产品表Id
     ask_uid:申请用户id,
     ask_date: 申请时间
     ask_description: 申请说明
     audit_uid: 审核人
     audit_date:审核日期
     audit_description: 审核描述
     status: 状态： 1.等审核,2通过，3未通过

>    服务器相关业务数据

	hostclients: 网站服务器业务数据(服务器数据表)
		hid: 自增序号
    product_id: 产品表Id
    server_id: 服务器表Id
    cabinet_server_id:所在机位
		mip_id: 管理IP(ID)
    ipb_id: 业务IP
		client_uid: 客户ID
		create: 创建时间
		equipment_date: 上架时间
		service_expired_date: 到期时间
		service_disabled_date: 停用时间
		last_uid: 最后修改管理员UID
		description: 备注
    trial: 试用
		init_pwd: 服务器密码
    unpaid_order: 未完成的定单
		status: 状态[待处理，处理中，待上架，已上架，已停用， 已下架]
    isbind: 已绑定
    online_op: 上机操作

  hostclient_handle_info: 服务器处理过程
    hid: 自增长
    handle_order_id: 订单id
    handle_order_product_id: 订单产品Id
    handle_action: 类型： 1租用2续费3升级
    client_description: 客户描述
    busi_uid: 业务部处理人
    busi_accept_data: 业务受理日期
    busi_complete_data: 业务完成日期
    busi_status: 业务处理状态
    tech_uid: 技术部处理人
	  tech_accept_data： 技术部受理日期
    tech_complete_data： 技术部完成日期
    tech_check_item： 技术部检查项
    tech_description： 技术部描述
    tech_status： 技术部状态
    hostclient_id: 所属客户服务器

  hostclient_business:
    hostclient_id: 所属客户服务器
    business_id: 所属业务，
    business_content: 业务内容


  
	hostclients_buss_log:(@todo 日志)
		id: 
		bid: 
		uid: 
		status:
		description: (业务|技术) 

	@todo(用配置预定义数据)
		技术->服务器的检查->几个状态
> 	服务器故障管理

	server_question_class: 故障分类
		id: 自增号
		class_name: 分类名称
		limited_stamp: 时间期限
		description: 描述
		parent: 所属分类(int[取自预先定义的术语分类[系统问题、网络问题、其他问题]])

	server_question: 故障问题
		id: 自增号
		parent_question_class: 故障分类ID(int)
		uid: 客户UID

		-------------create: 发布日期-------------

		status: 问题处理状态
		server_uid: 负责人ID(后台管理员UID)
		accept_stamp: 受理时间
		pre_finish_stamp: 预计完成时间
		finish_stamp: 完成时间
		mipstring: 客户提交的IP列表的管理IP存储
		ipstring: 客户提交的IP列表（varchar(1024))
		content: 问题内容

	server_question_detail: 故障问题详情
		question_id: 问题编号
		creat: 问题回复时间
		uid: 回复UID
		content: 回复内容
 ++flags 回复信息的类型 前台/后台 0后台

	server_question_convert: 故障问题变更
   ++id 记录编号
		from_uid: 转出人UID
		to_uid: 转入人UID
		from_stamp: 转出时间戳
		to_stamp: 转入时间戳
		question_id: 问题编号

    uid: 客户UID    //可以从问题表中读取	

		description: 问题转出描

===================================================
server_question_class_log: 故障问题分类变更日志
		id: 自增ID
		from_class: 变更前分类
		to_class: 变更后分类
		server_uid: 变更人UID
		to_stamp: 变更时间
		question_id: 问题编号


