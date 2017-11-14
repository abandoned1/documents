1. 定义{theme}.info.yml
  eg:
  name: Fluffiness
  type: theme
  description: 'A cuddly theme that offers extra fluffiness.'
  package: Custom
  core: 8.x
  stylesheets:
    all:
      - css/layout.css
    print:
      - css/print.css
  stylesheets-remove:
    - normalize.css
  regions:
    header: Header
    content: Content
    sidebar_first: 'Sidebar first'
    footer: Footer

2. 主题文件结构
  |-core
  |  |-modules
  |  |-themes
  |  |  |-bartik
  |  |  |-seven
  ..
  |-modules
  |-themes
  |  |-contrib
  |  |  |-zen
  |  |  |-basic
  |  |  |-bluemarine
  |  |-custom
  |  |  |-fluffiness

  下面是一个典型的主题文件结构布局:
  |-fluffiness.breakpoints.yml 定义不同设备的响应设计
  |-fluffiness.info.yml 必须的,在该文件中定义了元数据，样式，分区等.
  |-fluffiness.libraries.yml 这个用于定义主题需要加载的JS
  |-fluffiness.theme 这是一个PHP文件，定义了条件逻辑和数据(预)处理的输出
  |-config
  |  |-install
  |  |  |-fluffiness.settings.yml
  |  |-schema
  |  |  |-fluffiness.schema.yml
  |-css
  |  |-style.css
  |-js
  |  |-fluffiness.js
  |-images
  |  |-buttons.png
  |-logo.png
  |-screenshot.png
  |-templates 
  |  |-maintenance-page.html.twig
  |  |-node.html.twig

3. 使用Twig模板
  1) 覆写模板需要处理以下步骤:
    a. 找到你想覆盖的模板
    b. 复制目标模板到自己的主题中
    c. (可选) 根据命名规则重命名模板
    d. 根据需要修改模板
    可以使用Twig调试工具来验证需要处理的模板的位置.
  2) 主题钩子的建议
   有时你想更改的模板文件，但仅限于一些使用它的地方。
   一个常见的例子是改变的一个特定类型的节点的节点的模板文件。
   Drupal的主题层，您可以以具体使用情况通过以下特定的命名约定为目标的模板文件。当渲染一个文章节点时，Drupal会首先查找node--article.html.twig模板文件，如果存在，则使用它。如果不存在，则回滚到node.html.twig模板。这个过程通过Drupal来决定可能的模板文件，并使用theme hook suggestions.
   主题钩子函数允许你在你的主题中为指定文件名的模板实现重载一个目标模板.
  从核心，模块，主题都可以提供一个suggestions.你可以使用下面的钩子来添加或修改suggestions.
  a. hook_theme_suggestions_HOOK(array $variables)
  b. hook_theme_suggestions_alter(array &$suggestions, array $variables, $hook)
  c. hook_theme_suggestions_HOOK_alter(array &$suggestions, array $variables)
  
  3) 重建缓存
  有时应用新建的模板时，需要清缓存。

  4) 背景知识
  你可以把suggestions当作命名提示来告知系统来挑选，并在合适的情况下选取。该模板的suggestions是通过主题suggestions钩子可以改变设定。这些钩子允许任何模块或主题，提供可供选择的主题功能或模板名称的建议和重新排序或删除由hook_theme_suggestions_HOOK（）或更早的这个钩子调用所提供的建议。

  5) Drupal如何确定基于路径页面主题挂钩的建议

