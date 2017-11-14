1. contact us
  allowed page: 'contact'
2. Main menu navigation:
  hide page: 'user/*'

3. Member menu navigation:
  allowed page: 'user/*'
4. 禁用User account menu菜单项:
    My account禁用
5. 会员中心-账号管理:
  allowed page:
    user/account
    user/account/*
   会员中心-订单管理:
    user/order
   会员中心-我的服务:
   user/malfunction/declare
   user/malfunction
   user/server
6. 文章列表区块:
    allowed page:
      publish/articles/*
      node/*
7. 新闻列表区块:
    allowed page:
      publish/news/*
      node/*
8. 文章推荐列表:
    allowed page:
      publish/articles/*
      publish/news/*
      node/*
9.配置用户注册是否要通过邮件激活。
  路径：http://hostspaces.local.host/admin/config/people/accounts
  操作：1.Who can register accounts? 改为：Visitors.
        2.去掉Require email verification when a visitor creates an account前面的勾。
10.登录后，网页top用户名提示没有变。
  路径：http://hostspaces.local.host/admin/structure/block/manage/xunyun_login_tip
  操作： 1.将Cache settings里的Maximum age改为no caching;

  
