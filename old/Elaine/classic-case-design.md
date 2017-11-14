*classic-case-design*classic-case(经典案例)
说明：
	1.对经典案例分类进行列表展示
	2.对经典案例进行列表展示

问题：
需求问题
1.案例分类
	a)案例类型列表展示(案例分类名称，统计[该分类下有几天案例])
	b)案例类型编辑(修改类型名称)
	c)案例类型添加(类型名称)
	d)案例类型删除
2.案例
	a)经典案例列表展示(客户名称，案例分类，更新日期)
	b)案例信息编辑，添加新案例(名称，网站域名，所属分类,显示序号,效果预览图,效果全图,是否首页显示)
	c)案例删除


一、 系统变量 ~

二、 请求设计 ~ 

三、 权限设计 ~

四、 对象设计 ~

五、 数据库设计 ~
	A)case_catalog(案例分类)
		catalog_id：分类id(主键) 	int
		catalog_name:分类名称	varchar(20)
	B)case(案列)
		case_id:案例编号(主键)	int
		title:案例名称 	varchar(50)
		url:案例网站域名	varchar(255)
		picture_preview:预览效果图路径	varchar(255)
		picture_path:效果图路径		varchar(255)
		catalog_id:案例分类编号(外键，关联自案例分类表中的分类名称字段)	int
		savedatatime:更新日期(案例的最后修改日期) int
		order:显示序号	int
		index_show:是否首页显示(0 是 1否) 	tinyint

六、 APIs设计 ~

