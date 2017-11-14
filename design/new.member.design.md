网站用户的基础信息  
  uid       用户id  
  username  用户名
  mail      邮箱
  password  密码
-----------------
  regip     注册ip
  regdate   注册日期

员工详细信息
  uid           用户ID 外键  引用用户基础信息表中的主键id
  realname      姓名
  department    部门
  position      职位
  qq            QQ号码
  telphone      联系电话
  address       详细地址

会员详细信息
  uid              用户ID 外键  引用用户基础信息表中的主键id
  nick             用户昵称
  client_name      姓名
  user_picture     用户头像(integer)
  corporate_name   公司名称
  client_type      会员类型 (企业｜个人)
  industry         行业分类(术语)
  major_bussiness  主营业务(string)
  security_level   账号密码安全级别(术语|弱中强)
  safe_question    密保问题           |(string)
  safe_answer      密保答案           |(string)
  safe_question_1  密保问题           |密保(string)
  safe_answer_1    密保答案           |问题(string)
  safe_question_2  密保问题           |及(string)
  safe_answer_2    密保答案           |答案(string)
  province         省份 (术语)
  city             城市 (术语)
  region           县 (术语)
  address          具体地址(string)
  qq               QQ(string)
  telephone        固定电话(string)
  fax              传真(string)

 ++ commissioner  客服专员

会员公司下的子帐号  user_client_child_account
  id        自增主键
  parent    所属的父帐号id
  relname   姓名
 --- password  密码
 --- mail      邮箱
  dept      所属部门(该部门是网站会员公司的部门)

信用额度/现金余额管理  user_funds_data
  id         编号 主键
  uid        用户id
  cash       现金余额
  credit     信用额度
  alarm      预警开关   on/off  [三种提醒方式：E-mail邮件提醒 站内信提醒  会员中心谈框提醒]

代理信用额度提升/操作记录 user_funds_op_record
  id       编号
  amount   操作金额
  message  操作内容
  client_uid   客户id
  op_uid       操作用户id
  created      操作时间
