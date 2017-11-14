*employees-design* employees(员工)

说明：
	1.对公司员工进行管理

问题
需求问题：
	1.员工分类需求
		a)员工分类列表展示(编号，名称，性质，是否超级管理员，统计此分类下的员工数)
		b)员工分类信息删除
		c)员工分类信息添加(名称，是否默认群组，群组性质，事都超级管理员组)
	2.员工需求问题
		a)员工信息列表展示(编号，email,用户id，全名，QQ，电话，地址，部门)	
		b)员工信息编辑(姓名，邮箱，QQ，地址，职位，手机，描述)
		c)员工信息删除
		d)员工信息条件搜索(姓名，邮箱，QQ，用户名，地址，电话，部门)
		e)添加员工(账号，部门，密码，email)
	
一、 系统变量 ~

二、 请求设计 ~ 

三、 权限设计 ~

四、 对象设计 ~

五、 数据库设计 ~
staff_dept(部门)
	dept_id:部门编号 (主键)	int
	name:部门名称 varchar(20)
	id_parent_dept:上级部门	int
	description:描述	varchar(60)

positions(职位)
	p_id:职位编号(主键)	int
	name:职位名称	varchar(20)
	dept:所属部门(外键,引用部门表中的部门编号) int		
	description:描述	varchar(60)

employees(员工)
	id_employee:员工编号(主键)	int
	username:员工账号	varchar(12)
	password:登录密码	varchar(16)
	dept:部门 	(外键 引用部门表中主键)	int
	positions:职位 	(外键 引用职位表中主键)	int
	fullname:姓名 	varcha(12)
	email:邮箱	varchar(60)
	QQ:QQ号码	varchar(15)
	tel:电话号码	varchar(11)
	address:地址 	varchar(255)
	description:描述	varchar(100)
	savedatetime:保存时间	int
	lastlogintime；上次登录时间		int
	logincount:登录次数		int

	六、 APIs设计 ~