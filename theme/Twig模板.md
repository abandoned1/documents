##使用Twig模板

###重载模板
    可以按照模板的命名规则在主题文件夹里新增模板文件。

    1. 定位希望重载的模板文件
    2. 从基础模板位置复制模板文件到自定义的主题文件夹。
    3. (可选) 根据命名规则重新定义
    4. 修改模板

###Theme hook suggestions
	有时需要对某个模板的部分做修改。一个通用的示例对node的特定模板做修改。
	当渲染一个arctile类型的节点时，Ｄrupal将会首先查找node--article.html.twig模板，如果不存在，则会返回到node.html.twig模板文件。
	Drupal通过调用theme hook suggestions来决定调用哪一个模板。
	所有从核心，模块，主题等可以提供suggestions.你可以通过使用下面的钩子修改suggestions:
	1. hook_theme_suggestions_HOOK(array $variables)
	2. hook_theme_suggestions_alter(array &$suggestions, array $variables, $hook)
	3. hook_theme_suggestions_HOOK_alter(array &$suggestins, array $variables)

### Rebuild cache
	构建模板需要注意重清缓存。
### Background information
	你可以把suggestions当作命名提示，以便告诉系统基于正确的循环来选择和拾取。
	模板的suggestions可以通过theme suggestion hooks来修改。这些钩子通过hook_theme_suggestions_HOOK()允许任何模块或主题来修改主题function或模板名suggestions或reorder或remove suggestions,或者更早的调用这些钩子。

### 基于路径Drupal是怎样调用theme hook suggestions
	这里有个关于theme_get_suggestions的另外一种解释:
	Drupal通过theme_get_suggestions()对给定的页面生成一个可用的模板列表，这个调用了system_theme_suggestions_page().
	这个页面的Drupal路径拆分进组件。正如上面提到的,Drupal路径不仅是它的别名:它是该页面仅有的Drupal路径。例如"http://www.example.com/node/1/edit" and "http://www.example.com/mysitename?q=node/1/edit",
	Drupal的路径是node/1/edit,组件是"node",1,"edit".

	下一步，前缀被设置到"page",然后对每个组件，下面的逻辑如下:
	1. 如果组件是一个数字，添加前缀"__%"到suggestions列表.
	2. 无论组件是否是一个数字，添加一个下划线前缀到suggestions的组件列表里。
	3. 如果组件不是一个数字，添加一个"__"的前缀到组件里。

	Note that eventually, to turn a suggestion into an actual file name, "__" gets turned into "--", and ".html.twig" gets appended to the suggestion. Thus, for node/1/edit, we get the following list of suggestions:
	1. page.html.twig(always a suggestion)
	2. page--node.html.twig(and prefix is set to page__node)
	3. page--node--%.html.twig
	4. page--node--1.html.twig(prefix is not changed because the component is a number)
	5. page--node--edit.html.twig(and prefix is set to page__node_edit)
	6. page--front.html.twig(but only if node/1/edit is the front page)

	当页面被渲染后，最后的suggestion被检查。如果存在，那suggestion将被使用。否则下一个suggestion将被检查，等等。当然，如果没有重载的模板，最终将会调用page.html.twig模板。

### 和Drupal7的不同
	相对以前的模板修改，你可以修改preprocess函数中的$variables['theme_hook_suggestion']和$variables['theme_hook_suggestions']来介绍theme suggestions.在Drupal8中，模板和主题现在它们专用的钩子中定义和修改theme suggestions。


---------------

## 在Twig模板中发现和注入变量
在模板中,Twig提供了一个dump函数来发现模板文件中的变量.dump函数必须在debugging启用的情况下.

###打印一个独立的变量
`{{ dump(title) }}`
###发现模板中的所有变量
`{{ dump() }}`
    打印所有变量包含key的值:
`{{ dump(_context|keys) }}
	存在一些Twig的全局变量,如下:
	_self:
	_context: 
	_charset: 当前模板的编码格式

###dump()提示
	如果你想查看所有的变量,但dump()结果在消耗内存,可以像下面这样查看_context的所有键:
`<ol>`
`	{% for key, value in _context %}`
`		<li> {{ key }} </li>`
`	{% endfor %}`
`</ol>`
	**Then** use a conditional to check (for example {{ if loop.index = 2 %}), and dump that value only if necessary.



















