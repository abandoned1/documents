文章管理库 设计
目的:
1. 保存网站发布的所有文章数据

设计思想:
1. yml文件配置定义好文章相关的所有基础属性
2. Node节点配置文章/新闻所需的字段
3. node.type.*.yml配置分类(文章/新闻)
4. filed.storage.*.*.yml文件配置字段
5. fied.field.*.*.*.yml文件将字段绑定在分类上
6. 用术语来处理文章/新闻的栏目

一、系统变量

二、请求设计


三、权限设计
	administer published_info list
	administer published_info add
	administer published_info edit
	administer published_info delete	

四、对象设计

五、数据库设计

category  新闻栏目  术语  对应的术语是：newsCategory
article_category  文章栏目  术语  对应的术语是:articleCategory

文章/新闻公用的配置字段：
  view  浏览量   默认为0  前台浏览一次自动累加1
  copyright  版权   默认 HOSTSPACE
  key_words  关键字     多个的情况要求以半角逗号隔开
  summary    摘要     
