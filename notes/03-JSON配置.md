# JSON配置 

在小程序中, JSON扮演的静态配置的角色. 常见的有下面的几种配置文件. 

* app.json: 小程序的全局配置文件, 包括了小程序的所有页面路径、界面表现、网络超时时间、底部 tab.
* 页面配置信息: 每个页面的配置信息. 该配置信息只作用于当前页面
* project.config.json: 项目配置信息.
* sitemap.json: 

## 全局配置参数

* entryPagePath: 小程序启动页面路由
* pages: 小程序所有页面路由集合
* window: 用于设置小程序的状态栏、导航条、标题、窗口背景色
  * navigationBarBackgroundColor: 导航栏背景颜色
  * navigationBarTextStyle: 导航栏标题样式, 仅支持black和white两种样式
  * navigationBarTitleText: 导航栏标题
  * navigationStyle: 导航栏样式, 支持default和custom 2中样式, 默认为default, 微信会为小程序提供一个导航栏和右上角的小程序设置和关闭按钮. 值为custom的时候, 只有右上角的按钮, 没有navigationBar. 
  * backgroundColor: 窗口的背景色
  * backgroundColorTop: 顶部窗口的背景色
  * backgroundColorBottom: 底部窗口的背景色
  * enablePullDownRefresh: 是否开启全局的下拉刷新, 默认为false
  * onReachBottomDistance: 页面上拉触底事件触发时距页面底部距离, 单位为px. 
  * pageOrientation: 页面旋转设置. auto: 跟随手机屏幕的旋转而旋转, portrait: 页面竖着显示. landscape: 页面横着显示
* tabBar: 设置底部标签栏, 值为一个对象, 对象的key说明如下:
  * color: 标签栏文字颜色
  * selectedColor: 选中的标签的文字颜色
  * backgroundColor: 标签栏的背景颜色
  * borderStyle: 标签栏上边框的样式, 仅支持black和white两种样式, 默认为black. 
  * position: tabBar的位置, 仅支持top和bottom, 默认为bottom在底部显示
  * custom: 是否自定义tabBar
  * list: 定义tabBar items, 值为一个数组, 数组中的项为一个对象. tabBar最少配置2个tabBar item, 最多5个.
    * text: tabBar item的文字
    * pagePath: 每个tabBar item对应的页面的路由
    * iconPath: tabBar item没有被选中时的图片, tabBar position在顶部的时候不显示图片.
    * selectedIconPath: tabBar item选中时的图片
* networkTimeout: 网络超时设置
  * request: wx.request的超时时间
  * connectSocket: wx.connectSocket的超时时间
  * uploadFile: wx.uploadFile的超时时间
  * downloadFile: wx.downloadFile
* debug: 是否开启调试模式
* functionalPage: 插件所有者小程序需要设置这一项来启用插件功能页
* subPackages: 声明项目分包结构
* workers: 使用 Worker 处理多线程任务时, 设置 Worker 代码放置的目录
* requiredBackgroundModes: 申明需要后台运行的能力, 类型为数组. 目前只支持 audio: 后台音乐播放和location: 后台定位
* plugins: 申明小程序需要使用的插件
* preloadRule: 申明分包预下载的规则
* resizable: 在iPad上运行的小程序可以设置支持屏幕旋转; 在PC上运行的小程序, 用户可以按照任意比例拖动窗口大小, 也可以在小程序菜单中最大化窗口. 
* usingComponents: 声明视为全局的自定义组件, 在页面内部中可以直接使用不用在去声明
* permission: 隐私权限授权相关设置
* sitemapLocation: 指定sitemap.json的位置
* style: 指定基础组件样式的版本
* useExtendedLib: 指定需要引用的扩展库
* entranceDeclare: 聊天位置消息用打车类小程序打开
* darkmode: 适配暗黑模式
* themeLocation: 自定义theme.json的路径
* lazyCodeLoading: 通常情况下, 在小程序启动期间, 所有页面及自定义组件的代码都会进行注入, 当前页面没有使用到的自定义组件和页面在注入后其实并没有被使用. 自基础库版本 2.11.1 起, 小程序支持有选择地注入必要的代码, 以降低小程序的启动时间和运行时内存.
* singlePage: 单页模式相关配置, 目前分享到朋友圈后打开会进入单页模式

## 页面配置参数

小程序页面也可以使用页面的.json文件来对本页面的窗口表现进行配置. 页面中配置项在当前页面会覆盖 app.json的window中相同的配置项. 页面配置项基本都能在全局配置项中找到, 页面配置项会覆盖全局配置项的设置. 

* disableScroll: 设置页面整体能否上下滚动, 默认为false. 该配置项只能在页面配置json文件中设置, 而不能在app.json中设置. 

## sitemap配置

小程序根目录下的 sitemap.json 文件用于配置小程序及其页面是否允许被微信索引, 文件内容为一个 JSON 对象, 如果没有 sitemap.json, 则默认为所有页面都允许被索引; sitemap.json 有以下属性.
* rules: rule配置项指定了索引规则, 每项规则为一个JSON对象, rule配置说明如下: 
  * action: 页面是否能被索引, allow为可以被索引, disallow为不可以被索引. 默认值为allow
  * page: 页面路由, *表示所有页面.
  * params: 当page字段指定的页面在被本规则匹配时可能使用的页面参数名称的列表.
  * matching: 匹配规则的值. 每个值说明如下
    * exact: 当小程序页面的参数列表等于 params 时, 规则命中.
    * inclusive: 当小程序页面的参数列表包含 params 时, 规则命中
    * exclusive: 当小程序页面的参数列表与 params 交集为空时, 规则命中
    * partial: 当小程序页面的参数列表与 params 交集不为空时, 规则命中
  * priority: 匹配优先级, 值越大规则越早被匹配, 否则默认从上到下匹配.








    

