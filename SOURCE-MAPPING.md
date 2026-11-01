# BewlyCat 设置对应表

核对仓库：`keleus/BewlyCat`。固定提交：`f11de77051bbc8896f9038e51cc3af88e737cc5c`。这些是跨网站的功能对应，并非声称两个插件使用相同 DOM 或相同设置文件。

## 已提供的设置

| 本扩展设置 | BewlyCat 字段 | 源码路径（该提交） | 本扩展默认值 / 适配范围 |
| --- | --- | --- | --- |
| 启用悬浮导航 | alwaysUseDock | [DockAndSidebar.vue](https://github.com/keleus/BewlyCat/blob/f11de77051bbc8896f9038e51cc3af88e737cc5c/src/components/Settings/PluginComponentsAndPages/DockAndSidebar/DockAndSidebar.vue) | 开；关闭后恢复此前边缘展开的侧栏 |
| 导航位置 | dockPosition | 同上 | 左；支持左、右、底部 |
| 自动收起 / 收起一半 | autoHideDock / halfHideDock | 同上 | 关；两者互斥 |
| 显示的入口 | dockItemsConfig.visible | 同上 | 通知关，精选/推荐/关注/朋友/消息/我的开；至少保留一个 |
| 各宽度下列数 | gridColumns | [VideoCard.vue](https://github.com/keleus/BewlyCat/blob/f11de77051bbc8896f9038e51cc3af88e737cc5c/src/components/Settings/PluginComponentsAndPages/VideoCard/VideoCard.vue) | 六个断点均为 3；可设 1–12 列 |
| 悬停预览 | enableVideoPreview | 同上 | 开；关闭时阻止卡片悬停播放并暂停已有卡片预览 |
| 预览控制条 | enableVideoCtrlBarOnVideoCard | 同上 | 开；此前选定的两个预览图标仍按固定规则隐藏 |
| 标题字号 | videoCardTitleFontSize | 同上 | base，14px；xs/sm/base/lg 适配为 12/13/14/16px |
| 显示顶部搜索区域 | enableTopBar | [TopBarVisualConfig.vue](https://github.com/keleus/BewlyCat/blob/f11de77051bbc8896f9038e51cc3af88e737cc5c/src/components/Settings/PluginComponentsAndPages/TopBar/TopBarVisualConfig.vue) | 开 |
| 顶部显示方式 | otherPageTopBarConfig | 同上及 [storage.ts](https://github.com/keleus/BewlyCat/blob/f11de77051bbc8896f9038e51cc3af88e737cc5c/src/logic/storage.ts) | 下滚隐藏、上滚浮现；另有始终显示/悬停显示。本扩展同时延续首页分类收起行为 |
| 强调色 / 基准色 | themeColor / darkModeBaseColor | [Appearance.vue](https://github.com/keleus/BewlyCat/blob/f11de77051bbc8896f9038e51cc3af88e737cc5c/src/components/Settings/Appearance/Appearance.vue) | #35b5d5 / #20212b；作用于本扩展导航、搜索框与分类，不重写所有原生页面颜色 |
| 毛玻璃 / 关闭阴影 | enableFrostedGlass / disableShadow | 同上 | 毛玻璃关，关闭阴影开；限导航和搜索区域 |
| 详情页小窗按钮 | showVideoPipButton | [VideoPlayback.vue](https://github.com/keleus/BewlyCat/blob/f11de77051bbc8896f9038e51cc3af88e737cc5c/src/components/Settings/BilibiliFeaturesEnhancement/VideoPlayback/VideoPlayback.vue) | 开；不改变此前隐藏卡片预览小窗的规则 |
| 全屏滚轮音量 / 步长 | customFullscreenWheelVolume / fullscreenWheelVolumeStep | 同上 | 关 / 5%；仅浏览器原生全屏，普通首页不接管滚轮 |

断点采用 [storage.ts 的 GRID_BREAKPOINTS](https://github.com/keleus/BewlyCat/blob/f11de77051bbc8896f9038e51cc3af88e737cc5c/src/logic/storage.ts)：base <640、sm ≥640、md ≥768、lg ≥1024、xl ≥1280、xxl ≥1536。BewlyCat 自身默认 1/2/3/4/5/6；本扩展按用户要求默认全部三列。

## 沿用既定效果，不新增伪对应开关

在本次核对的相关设置组件中，没有确认到下列抖音专属行为的等价独立开关。因此不以相近名字冒充对应功能：

- 隐藏投稿、客户端推广、十个抖音分类、左侧 AI抖音/活动/直播/放映厅/短剧/小游戏/反馈入口。
- 隐藏个人菜单“创作者中心、我的预约、我的订单”。
- 隐藏详情点赞、收藏、听抖音、更多、弹幕输入框和倍速入口；预览隐藏指定两个图标。
- 仅保留搜索放大镜、隐藏占位文字。BewlyCat 的 showSearchRecommendation 控制搜索推荐，不等于占位文字，故未冒用该字段。
- 固定在最右侧的滚动条、对称留白、播放与时间靠左、其余控制项靠右、消息面板为视频让位。
- 去除底部刷新及分隔线。未把 BewlyCat 的返回顶部设置误称为“刷新”开关。

这些项目均保留本次对话最后确认的效果。尚未定位的个人主页深色区域作为已知问题保留，没有将未知遮罩直接删掉。

## 未迁移的无关功能

没有添加 B 站推荐 API、UP 主过滤、会员功能、合集、B 站专属弹幕设置、云同步或本次未请求的功能。外部稍后再看按钮的 externalWatchLaterButton 并不等于隐藏抖音按钮，未直接套用。

设置存储参考了“默认值、校验、配置变更通知”的组织原则，使用独立的 `chrome.storage.local` 实现；未复制 BewlyCat 的 Pinia/Vue 存储协调器。

## 2.0.2 用户指定的调整

按用户后续要求移除“颜色与质感”及四项外观设置，恢复固定基准配色、无毛玻璃、无阴影；即使 BewlyCat 有对应设置也不再展示。升级旧配置时恢复顶部搜索显示，之后在新版主动关闭仍会正常保存。标题和轻量预览控制条增加结构识别；顶栏滚动增加重排保护。

## 2.0.3 用户新增需求

用户明确要求分类独立开关、搜索入口和自由排序：增加 homeCategoriesConfig、dockOrder，并扩展 dockItemsConfig。排序交互对应 BewlyCat DockAndSidebar 中的可拖动入口配置；抖音分类与搜索入口是本扩展的网站适配，未冒充上游的相同字段。新版取消详情页边缘弹出侧栏，隐藏个人页投稿，保护个人信息容器不被背景清理误删。
