*member-design*	client(用户)

说明：会员管理

问题
需求问题
	1.会员组需求
		a)会员组列表展示(编号，名称，是否默认组，统计各群组下的会员数量)
		b)会员组信息修改(名称，是否默认组)
		c)新增会员组(名称。是否默认组，性质)
		d)会员组删除
	2.会员管理需求
		a)会员信息列表展示(会员ID，全名，区域，所属组，验证状态，注册日期)
		b)会员信息编辑(会员级别)
		c)删除，锁定/解锁会员账号
		d)会员搜索(账号，全名，email，所属群组，注册日期)
		e)添加会员(账号，群组，密码)
预备术语:
  学历: 初中及以下
        中专
        高中
        专科
        大学
        硕士
        博士
  职业: 学生
        国企员工
        外企员工
        自由职业
        其他
  客户级别:
        同行客户
        VIP客户
        潜在客户
        正式客户
  地区: 重庆
        深圳
        上海
        北京
        ...
  客户状态: 公有
            私有



一、 系统变量 ~

二、 请求设计 ~ 
login: (nocache) 用户登录, 替换 user/login
resetpwd: (nocache) 填写帐号信息，替换 user/password
resetpwd/sended: (nocache) 重置密码 在这里传入随机码参数，uid。在数据库里去找有无记录 没有就失效。
resetpwd/reset:(nocache) 重写密码(邮件中的地址) 替换 user/reset/%/%/%
user/edit: (nocache) 个人资料
user/resetpwd: (nocache) 特定用户密码修改
三、 权限设计 ~
会用到 user 模块提供的权限: administer users
四、 对象设计 ~
修改现有user对象，添加以下属性:
account: account对象
nickname: 昵称(在没有 account->nickname 的情况下，其值为 user->name)
五、 数据库设计 ~
member_group(会员组)
	id_group:会员组编号(主键)	int
	name:会员组名称		varchar(20)
	isdefault:是否默认会员组(0是 1不是)	tinyint
	type:会员组类型(性质)	varchar(10)

members(会员)
	mid:会员编号(主键)	int
	account:用户账号	varchar(12)
	password:登录密码	varchar(16)
	islock:是否锁定	(0是 1否)	tinyint
	email:邮箱	varchar(200)
	regIP:注册IP地址	varchar(50)
	regdate:注册时间	int

member_detail(会员详情)
	mid:会员编号(外键，引用会员表中会员编号字段)	int
	id_group:会员所属组(外键  引用会员组中主键)		int
	realname:真实姓名	varchar(10)
	QQ:QQ	varchar(20)
	tel:电话	int
	fax:传真	varchar(20)
	company:公司	varchar(60)
	website:网站	varchar(100)
	provice:省份	varchar(200)
	city:城市		varchar(200)
	address:地址	varchar(255)	
	zipcode:邮政编码	varchar(15)
	resetpassword:重置的密码	varchar(16)
	forgetpasswordsecurity:找回密码时的安全码	varchar(32)


六、 APIs设计 ~
