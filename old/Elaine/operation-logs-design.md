*operation-logs-design* operation-logs(操作日志)

说明：
	1.展示网站操作日志

需求问题
	a)对网站日志进行列表展示(日志类型，操作员，日志分类，描述，操作日期)
	b)清空操作日志
	c)按日志分类,操作员，操作时间段，IP描述查找日志
	d)双击日志描述列，弹窗显示日志详情

一、 系统变量 ~

二、 请求设计 ~ 

三、 权限设计 ~

四、 对象设计 ~

五、 数据库设计 ~
operation_log(操作日志)
	lid:日志编号(主键)		int
	type:操作类型			varchar(10)
	user:操作用户(外键 引用自用户表的用户id)	int
	detail:日志详情	longtext
	createdtime:日志创建时间 	int



六、 APIs设计 ~