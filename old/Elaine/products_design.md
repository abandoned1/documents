*products_design*  products(产品)

说明
	1.显示产品列表
	2.添加，编辑，删除产品

需求问题
1.产品目录
	a)产品目录列表展示，(名称，统计[该目录下所有的产品数量],排序，添加日期)
	b)（批量）删除目录
	c)添加目录(名称，父级，排序)
	d)修改目录(名称，父级，排序，简介)
2.产品
	a)产品列表展示(编号，名称，价格，所属分类，自选配置，更新日期)
	b)价格设置(价格ID，价格标题，付款类型，是否默认值，价格单位，价格描述)
	c)产品编辑，添加(所属目录，名称，编号，规格，IP数，电源，宽带，CPU，硬盘，内存，基本信息，描述，首页描述，产品展示图片，机房，是否可自选配置，发布状态)
3.自选配置
	a)当前产品的信息展示(编号，所属目录)
	b)当前产品的所有自选配置列表展示(ID，描述，排序，配置目录，父级目录，月付价格，季付价格，半年付，年付)
	c)新增，修改自选配置(所属目录，描述，月付价格，季付价格，半年付，年付，排序)

一、 系统变量 ~

二、 请求设计 ~ 

三、 权限设计 ~

四、 对象设计 ~

五、 数据库设计 ~
products_catalog(产品目录)
	id_catalog:编号(主键)		int
	name:名称:		varchar(20)
	id_parent:父级编号	int
	description:描述 	varchar(255)
	ordernumber:排序 	int
	savesatetime:保存时间	int

products(产品)
	id_products:(主键)		int
	pid:产品编号	varchar(64)
	pname:产品名称	varchar(64)
	picture:产品图片	varchar(255)
	descrption:描述 	longtext
	detail:详情		longtext
	index_desc:首页描述	char(30)
	idcroom:机房(外键 引用机房表中的主键)		int
	id_catalog：所属分类(外键 引用自产品目录中的主键) int
	iscustomer:是否可自选配置(0是 1否)	tinyint
	ispublish:是否发布(0是 1否)		tinyint
	ishot:是否热卖(0是 1否)		tinyint
	size:规格		varchar(255)
	IP:IP数量		int
	bandwidth:带宽	char(20)
	CPU: CPU 	varchar(50)
	harddisk:硬盘	varchar(50)
	memery:内存		char(20)
	ordernumber:排序 int
	savedatetime:保存时间 	int
	lastmodifytime:最后修改时间	int

products_price(产品价格)
	price_id:价格编号( 主键)		int
	title:标题		varchar(20)
	id_product:产品(外键  引用产品表中主键)	int
	price:价格  int
	description:描述 varchar(200)
	unit:单位	char(50)
	paymethod:付费方式	(1年付	2半年付	3季付	4月付)	int

products_customer_catalog(自选配置目录)
	id_catalog_customer:编号(主键)	int
	title:名称 	varchar(50)
	id_parent_catalog_customer:父级 int
	orderNumber:排序 	int
	savedatetime:保存时间 	int

products_customer(自选配置)
	id_customer:自选配置编号(主键) 	int
	id_catalog_customer:自选配置所属目录(外键 引用配置目录中主键)	int
	id_products:所属产品(外键  引用产品表中主键)	int
	title:配置标题	varchar(120)
	price_month:月付价格 		int
	price_season:季付价格		int
	price_halfyear:半年付价格	int
	half_year:年付价格 		int
	savedatetime:保存时间 	int
	oedernumber:排序 	int

六、 APIs设计 ~