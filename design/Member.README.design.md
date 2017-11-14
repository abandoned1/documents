Member模块 会员模块设计说明

目的:
  1. 设置会员管理相关页面
    1.1 员工管理
      1.1.1 部门管理(转化成角色管理)
        1.1 部门列表(角色列表)
        1.2 部门编辑(角色编辑)
        1.3 员工编辑(用户信息编辑)
        1.4 员工列表(用户列表)
    1.2 客户管理
      2.1 客户列表(用户列表)
      2.2 客户编辑(用户信息编辑+额外的字段定义-根据需求原型用户信息字段列表添加)
  2. 企业账号管理
    2.1 子账号管理（注:个人账号转为企业账号后，有权限添加（或绑定)子账号。
    2.2 子账号的权限分配
  3. 站内信息(会员信息)
    3.1 站内成员短信处理.
说明:
  这个模块仅仅是为了修改User模块相关请求，并重构新的管理页面。
  不需要设计新的实体。      

*. 设计思路:
  1. 新建路由请求，重构列表页面。
  2. 对User添加新的字段，满足现有网站会员资料的需要。

一、 系统变量

二、请求设计
admin/member/section: 部门列表
admin/member/section/add: 增加部门
admin/member/section/{section}/edit: 部门编辑
admin/member/list: 会员列表(包括员工和客户列表)
admin/member/staff/add: 增加员工
admin/member/staff/{staff}/edit: 编辑员工
admin/member/client/add: 增加员工
admin/member/client/{staff}/edit: 编辑员工

以及前台各种请求:
member/.../...
....

三、权限设计
administer member section list: 
administer member section edit:
administer member section delete:
administer member list: 
administer member client edit:
administer member client delete:
administer member staff edit:
administer member staff delete:

以及前台各种权限:
....

四、对象设计

五、数据库设计
Message
================================================================================
id:信息序号
to_uid: 收信用户
title: 标题
body: 内容
from_uid: 发信用户
created: 

User 
================================================================================
User基础字段:
name: 用户名(别名)
mail: 账号(注册邮箱，用于取回密码等的安全邮箱)

User扩展表设计:
id: 
uid: 关联user表uid字段
nick: 昵称(姓名|联系人姓名)(string)

========*****========*****=======
//应该适用单独的表来管理用户的现金余额和信用额度
banlance: 现金余额
credit: 信用余额
alarm: 预警开关
========*****========*****=======

security_level: 账号密码安全级别(术语|弱中强)

safe_question: 密保问题           |(string)
safe_answer: 密保答案             |(string)
safe_question_1: 密保问题         |    密保(string)
safe_answer_1: 密保答案           |    问题(string)
safe_question_2: 密保问题         |     及(string)
safe_answer_2: 密保答案           |    答案(string)
user_picture: 用户头像(integer)
corporate_name: 公司名称 (string)
type: 会员类型 (企业｜个人)  员工类型不能登录前台下单。（术语)
industry: 行业分类(术语)

app_type: 应用类型|关联多种类型(如网页游戏、手机游戏、客户端游戏、门户网站等)(术语)

major_bussiness: 主营业务(string)
host: 网址(string)
province: 省份 (术语)
city: 城市 (术语)
region: 县 (术语)
address: 具体地址(string)
qq: QQ(string)
telephone: 固定电话(string)
fax: 传真(string)
parent_uid: 父账号(integer) 
department:部门(string)
position:职位(string)

user_category：用户的类型  员工 / 会员   1员工 2会员












