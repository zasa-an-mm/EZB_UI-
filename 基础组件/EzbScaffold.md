# EzbScaffold · 页面容器契约

> **范围：**当前新设计系统页面容器的配置、默认行为与覆盖优先级。整体组合关系见 [基础页面](基础页面.md)，导航栏内部规格见 [EzbAppBar](EzbAppBar.md)，颜色见 [AppColor](../Color/AppColor.md)。本文为代码现状契约，业务适配选择仍按业务页校准。

## §1 容器与默认值

1. `EzbScaffold` 是页面组件，内部组合 Flutter `Scaffold`；页面提供 `body`、导航配置和可选底栏。它不要求业务页面继承特定基类，也不绑定业务控制器或数据服务。
2. 页面背景默认 `bgBase`；传入非空 `backgroundColor` 时覆盖页面背景。背景覆盖不会同步修改 `EzbAppBar` 的背景，后者仍用 `bgBase`，也不会自动给正文子组件换色。
3. `bodyPadding` 默认四边为0；`scrollable` 默认false；`useSafeArea` 默认true；`resizeToAvoidBottomInset` 默认true。默认正文既没有16px外边距，也没有自动滚动，不能按设计稿假定已包含。
4. `hideAppBar` 默认false，`automaticallyImplyLeading` 默认true；`extendBody` 与 `extendBodyBehindAppBar` 默认false，`primary` 默认true。`title`、`subtitle`、`leading`、`onBack`、`action`、`appBar`、`body` 和 `bottomNavigationBar` 默认均为空。
5. 页面不提供正文时不会生成正文占位；满足滚动标题条件时，仍可以单独显示标题组，条件见§3。所有业务文案及辅助技术用途标签由调用方提供本地化内容。

## §2 顶部栏选择顺序

1. **首先检查隐藏开关：**`hideAppBar=true` 时始终不显示导航栏，即使同时传入自定义 `appBar`。便捷标题也不自动插入正文；需要展示的内容应由页面自行提供。
2. **其次检查自定义栏：**未隐藏且 `appBar` 非空时，使用该栏，覆盖便捷导航参数。容器不再将自己的 `title`、`subtitle`、`leading`、`onBack`、`backSemanticLabel` 或 `action` 合并到自定义栏；这些内容需在自定义栏自身配置。
3. **最后检查便捷参数：**没有自定义栏时，`title`、`subtitle`、`leading`、`onBack`、`action` 中任一非空，才进入自动组合 `EzbAppBar` 的分支。只配置 `backSemanticLabel` 或只让路由可返回，不会单独触发导航栏生成。
4. `title=''` 也是非空参数，可用于请求只含导航操作的栏；但滚动模式下仍会执行第5条的空栏省略判断。空字符串不显示文字。
5. 滚动模式下，没有自定义 `leading` 和 `action`，且自动返回已关闭，或没有显式 `onBack` 且路由不要求退出入口时，省略空白导航栏。标题仍可移入正文，不为没有操作的栏保留44px空位。
6. 自动生成的栏接收导航参数；非滚动模式同时传入标题、副标题，滚动模式则只在栏内保留导航操作。左右操作显示、回调与样式均按《EzbAppBar.md》。

## §3 标题进入正文与正文滚动

1. 当且仅当 `scrollable=true`、没有自定义 `appBar`、`hideAppBar=false`，并且标题或副标题至少有一项非空文字时，容器在正文最前面插入内置标题组。
2. 从上到下为内置标题、可选副标题、16px留白及业务 `body`。只有 `body` 非空才添加这16px；标题组内部规格按《EzbAppBar.md》§3，不随位置改变字号和颜色。
3. 上述组合内容放入 `SingleChildScrollView`，`bodyPadding` 作用于整组内容并随之滚动，不仅作用于业务 `body`。标题、说明与业务正文一起滚动；导航栏和底栏不在该区域内。
4. `scrollController` 仅在 `scrollable=true` 时传给该滚动区域，由调用方创建、持有和释放；非滚动模式不使用此参数。
5. `keyboardDismissBehavior` 默认manual，滚动不会主动按拖动收起键盘；传入其他行为时按配置执行。容器没有额外的点击空白收键盘逻辑，也不会自动滚到第一个校验错误。
6. `scrollable=false` 时，只在业务正文外添加 `bodyPadding`，不插入正文标题组，不增加滚动控件。业务正文可以自行使用列表、`Expanded` 或其他有界布局。

## §4 安全区与栏位高度

1. `useSafeArea=true` 且存在正文内容时，容器在正文最外层包裹 `SafeArea`，避让当前布局下剩余的设备安全区。导航栏、底栏与正文分别管理各自区域，不按设计图中的固定状态栏高度重复留白。
2. `useSafeArea=false` 只关闭正文的这层避让，不会关闭 `EzbAppBar` 自己的安全区，也不会自动让正文延伸到导航栏背后；是否延伸还需按第5条设置。
3. 对自动生成或自定义传入的 `EzbAppBar`，容器按当前宽度、系统字号和文字内容计算所需高度，再限制在可用页面高度的一半减去顶部占用范围以内；长文可在栏内部纵向滚动，避免导航栏挤占全部正文。
4. `primary=true` 时保留顶部系统栏处理；`primary=false` 时，容器会移除该 `EzbAppBar` 读取的顶部安全区，避免嵌套容器再次添加状态栏高度。其他类型的自定义导航栏按其自身实现处理。
5. `extendBody` 与 `extendBodyBehindAppBar` 原样交给内部 `Scaffold`，分别控制正文是否延伸到底栏或顶栏背后；两者不生成渐变或遮罩，也不自动关闭正文安全区。全屏相机、插画或渐变页需明确配置并自行处理内容对比度。
6. 组件不锁定设计基准画面的 y 坐标，也不自动加入业务顶部留白。KYC 标准导航下方到正文标题的14px由业务页面提供，使用正文顶部间距时仅计一次；顶部页面留白按 KYC 通用约定处理。本轮不修改或扩展本组件，分工见《基础页面.md》§5。

## §5 底部区域与键盘

1. `bottomNavigationBar` 为固定底部栏位，可承载底部操作区或底部导航。容器原样传入，不为其附加内边距、`SafeArea` 或业务按钮；底栏自行负责底部安全区。
2. `resizeToAvoidBottomInset=true` 时，正文按内部 `Scaffold` 的键盘避让机制缩小可用范围；它并不等于所有自定义底栏都会自动升到键盘上方。
3. 使用 `EzbBottomActionBar` 时，底栏需要读取键盘 `viewInsets`；不要在其外层再次叠加同一份键盘高度或重复移除 `viewInsets`。换成其他底栏时，必须明确该底栏的键盘处理方式。
4. `resizeToAvoidBottomInset=false` 时，关闭正文自动随键盘缩小。输入区、底栏和键盘重叠由页面自行协调，不适合作为所有表单的默认配置。
5. `bottomSheet`、`floatingActionButton`、`floatingActionButtonLocation`、`drawer`、`endDrawer` 直接传给内部 `Scaffold`；容器不替业务安排它们的内容、事件、样式和层间间距。

## §6 系统栏与页面访问

1. 未传 `systemOverlayStyle` 时，状态栏背景透明；状态栏与系统底部导航栏的图标明暗随主题设置，系统底部导航栏颜色使用当前页面背景。
2. 非空 `systemOverlayStyle` 覆盖本层整份默认配置，而不是逐个字段与默认对象合并。顶部 `EzbAppBar` 也有自己的局部系统栏配置，页面外层设置不能保证覆盖它；需要特殊状态栏效果时，按具体栏位统一配置。
3. `scaffoldKey` 提供访问内部 `ScaffoldState` 的入口，例如打开抽屉；未提供时使用普通内部容器。`restorationId` 原样传入，不代表已经实现业务表单或申请数据恢复。
4. 页面没有内置加载、失败、自动保存、退出确认、路由跳转或接口请求。上述逻辑由调用方实现；系统返回与按钮回调的边界见《基础页面.md》§4。

## §7 典型组合的配置要求

1. **标准可滚动表单：**使用容器滚动时，正文边距显式指定，底部操作放独立栏位。需要KYC大标题时，按业务要求在正文提供，并注意避免重复使用内置标题组。
2. **带列表或自定义剩余高度布局：**保持 `scrollable=false`，由正文自行管理滚动；不要因有长列表再在容器层重复开启滚动。
3. **结果页：**是否展示导航栏由页面契约指定；隐藏导航栏不自动移除正文安全区，也不自动为状态图形或标题安排顶部位置。
4. **全屏采集页：**根据页面要求选择关闭正文安全区、隐藏导航栏或使用自定义栏，并显式配置系统栏。采集权限、关闭行为及 SDK 控制范围不属于容器本身。
