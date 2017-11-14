*news-design"news(网站新闻)

说明
	1.对网站新闻进行列表展示
	2.对新闻组进行展示
	3.添加新闻

问题
需求问题
1.新闻
	a)新闻列表展示(标题，所属目录，发布状态，日期)。
	b)在列表页可直接设置新闻是否发布。删除新闻.根据新闻目录，查询指定目录下的新闻列表
	c)新闻详情预览
	d)新闻编辑(标题，是否滚动显示。所属目录，标题图像，描述，内容，编辑人，版权，是否发布)
	e)添加新闻(标题，是否滚动显示。所属目录，标题图像，描述，内容，编辑人，版权，是否发布)

2.新闻目录
	f)对新闻组进行树状展示(名称，排序)
	g)新闻组目录直接编辑名称，排序
	h)新闻分类目录编辑，(名称，所属上级目录，描述，是否前台显示)
	i)删除新闻分类目录.(若该目录下有新闻，则提示无法删除)
	j)查看是定分类目录下的新闻列表
	k)添加新闻组目录（名称）
	l)添加新闻分类目录(名称，所属上级目录)

一、 系统变量 ~

二、 请求设计 ~ 

三、 权限设计 ~

四、 对象设计 ~

五、 数据库设计 ~
news_catalog(新闻组)
	id_catalog:新闻组ID(主键)	int
	title:标题 	varchar(64)
	type:类型(新闻组 group , 新闻分类 catalog)	varchar(20)
	id_parent:父级编号.	int
	description:描述	longtext
	savedatetime：保存时间	int
	index_show:是否首页显示(0 是 1 否) tinyint
	compositor:显示顺序	int

news(新闻)
	id_news:新闻编号(主键) int
	id_catalog:所属分类编号 (外键 引用新闻组表中新闻组ID字段) 	int
	title:新闻标题	varchar(255)
	description:新闻描述	longtext
	content:新闻内容	longtext
	hits:新闻浏览量		int
	ispublish:是否发布(0是 1否) 	tinyint
	rights:版权	varchar(50)
	titlepicture:标题图片路径	varchar(255)
	editor:编辑人	varchar(20)
	idroll:受否首页滚动显示 	tinyint

六、 APIs设计 ~