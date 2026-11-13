# T1 · Payment Tab

> **状态：待校准，可先开发；真实接口联调完成后统一校准。** 本流程视觉规格见本流程内的视觉规格与逐屏规则。主方案为一张卡两行，空态为入口卡＋Add a payee，排除所有对比方案。

## 本流程视觉规格（待校准项就地标注）


1. **页面与导航：**普通表单和详情复用基础页面，背景 `bgBase`；正文左右16px，宽窗口最大560px。返回、关闭、系统返回及返回手势遵循本屏业务返回规则；未明确落点时标“（待校准）”，不自动套用 KYC 清空规则。正文标题22px / w700 / 行高28px / `textPrimary`；标题相对导航点击区域的垂直距离（待校准）。有副说明时使用15px / w400 / 行高20px / `textSecondary`；标题与副说明、首个内容的间距未单独列明者（待校准）。
2. **表单：**标准输入底 `bgField`、圆角16px、左右16px、上下14px；标签13px / w400 / 行高18px / `textSecondary`，下2px为值17px / w500 / 行高23px / `textPrimary`，占位 `textTertiary`。文字自撑高，最小高度（待校准）。聚焦2px `borderFocus`，标签 `textBrand`；错误辅助文案13px / w400 / 行高18px / `feedbackError`，与字段间距、错误背景及边框转换（待校准）。禁用 `bgDisabled`／`textDisabled`；只读保留正常文字颜色，不伪装成不可辨认的禁用态。未取得字段间距时逐屏标注，不默认照搬 KYC。
3. **金额：**当前开发采用正式34px / w700 / 行高40px、圆角16px；输入左右16px、上下14px，符号与金额间4px；符号 `textSecondary`，金额 `textPrimary`。设计曾为圆角14px，最终视觉匹配（待校准），不新增正式 token。余额／额度说明13px / w400 / 行高18px / `textSecondary`，距金额8px。
4. **主次操作：**主按钮最小高56px、圆角28px、文字17px / w600 / 行高23px；正常 `brandPrimary`／`textOnBrand`，禁用 `bgDisabled`／`textDisabled`。文字换行可增高，处理中阻止重复触发并播报状态；按下态复用正式按钮状态。次操作的具体表面、危险按钮颜色和相邻间距未明确者（待校准），不猜值。固定底部操作区与正文共用内容列，底部消费实时安全区；区域上下内边距（待校准）。
5. **半框：**背景表面语义、顶部圆角、标题到内容间距（待校准）；标题22px / w700 / 行高28px / `textPrimary`。宽窗口最大560px，矮窗口限高90%，内容内部滚动；操作和固定 Other 不被滚动区或系统栏遮挡。外点、下滑、系统返回是否关闭依各屏规则，未明确者（待校准）。
6. **行、详情与空态：**标准行最小高72px，上下8px；左40px图形容器、图形20px，与文字间12px。主文17px / w500 / 行高23px / `textPrimary`，副文15px / w400 / 行高20px / `textSecondary`，尾随箭头20px；头像字母15px / w600 / 行高20px。详情字段标签和值的布局、分隔线及行距未取得者（待校准），不能仅因复用组件省略差异。空态标题22px / w700 / 行高28px，说明15px / w400 / 行高20px；插画、对齐和间距依各屏，缺项（待校准）。
7. **适配与可访问性：**同名语义 token 分别映射明暗主题。支持100%／200%字号，长文自然换行；图标装饰不重复朗读，交互图标须有可读名称，独立点击区至少44px。310px窗口可用，安全区和键盘分别避让，底部导航、PIN删除键和主要操作不得被系统栏遮挡。


## §1 首页

1. **页面与导航：**本屏为 Payment Tab，不作为另一个重复首页。Home／Payment 底部导航保留，Payment 为当前项；导航图标、选中／未选中文字和玻璃表面的精确规格（待校准）。系统安全区由宿主与底部导航分别处理，正文滚动至最后一张卡不被底栏遮挡。
2. **顶部与卡片结构：**从上至下为 Logo／Payments、转账入口卡、Payees 或新增卡、定稿适用的 Cards。Payments 当前采用正式22px / w600 / 行高28px / `textPrimary`；原设计行高23px的视觉差异（待校准）。顶部 hero 资产、裁切、渐变与明暗组合（待校准），不由绝对 y 坐标固定布局。
3. **点击与数据：**入口卡两行分别进入行内账号页和海外银行页；联系人行进入对应金额页，星标独立操作。联系人名、尾号、最近交易金额／状态取同一份本轮资料，删除联系人不删除交易。
4. **离开与恢复：**切换 Home 后再回本页的滚动恢复与刷新时点（待校准）；当前主题／窗口变化不清空本轮联系人和交易。

**逐元素与状态细则：**

1. 顶部Logo与“Payments”，背景与首页同套hero；底部Home／Payment导航，Payment选中。已读主屏标题22/w600/行高23，与正式22/28存在冲突。Logo、背景复用现有同款资产，不自行重绘；黄色定稿框不是应用UI。
2. 主屏参考正文从y134起、左右16，入口卡铺满内容列，圆角20、底bgSurfaceRaised、设计模糊13，卡内左右16、上下4。相邻卡间16。实际顶部偏移按基础导航与安全区组合，不能固定状态栏54后照搬y坐标。hero遮罩及模糊与已有组件匹配（待校准）。
3. 入口顺序固定：Send to an EZB account，副文Free · Arrives instantly；Send to another bank，副文SWIFT · USD。行规格见本流程内的规格与规则，第一行去T2-00，第二行去T3-01。Free不构成永久免费业务规则，见本页对应的“（待校准）”项。图中行内图形语义为账户／用户确认，海外为globe；精确资源名及图标颜色待逐项读取（待校准），不猜映射。
4. Payees卡位于入口卡下16，圆角20、左右16、顶部16；标题Payees为15/w500/20/textSecondary。每人一行，左首字母图形40，主文姓名或昵称17/w500/23/textPrimary，副文15/w400/20/textSecondary；尾随星标与chevron分别为操作和去向，不让点星标误触发转账。
5. 联系人最多3条；星标在前，其余按最近转出／添加排序。只要有至少1个联系人，就显示See all，不以满3个为条件。See all高52、文字17/w500/23/textBrand，进入T4.1。星标组内部顺序及与T4“最近往来”的不同口径（待校准）。
6. 点击联系人进入对应金额页；如邮箱已变化，先确认；账户已失效则提示并移除，历史交易保留。副文示例Last sent {金额} · {日期}，SWIFT处理中示例SWIFT · {金额} · In progress；示例金额、姓名、时间不是默认Mock业务值。


### T1-01 Payments 首页 · 状态文案与属性（待校准）


#### 方案 1（方案 E）· 有余额 · 有收款人（1802:2746）

已取得详细上下文；完整视觉与交互仍待校准。

| 已读显示文本（动态样例不作为默认值） | 文字属性原始读取 |
| --- | --- |
| Payments | 22px / w600（设计可变字重590） / 行高23px / text/primary |
| Send to an EZB account | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Free · Arrives instantly | 15px / w400 / 行高20px / text/secondary |
| Send to another bank | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| SWIFT · USD | 15px / w400 / 行高20px / text/secondary |
| Payees | 15px / w500（设计可变字重510） / 行高20px / text/secondary |
| AA | 15px / w600（设计可变字重590） / 行高20px / text/primary |
| Ahmed Ali | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Last sent $1,200.00 · 28 Sep | 15px / w400 / 行高20px / text/secondary |
| AM | 15px / w600（设计可变字重590） / 行高20px / text/primary |
| AL MANSOORI TRADING | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| SWIFT · $8,500.00 · In progress | 15px / w400 / 行高20px / text/secondary |
| LT | 15px / w600（设计可变字重590） / 行高20px / text/primary |
| Lina Tan | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Last sent $450.00 · 20 Sep | 15px / w400 / 行高20px / text/secondary |
| Home | 11px / w500（设计可变字重510） / 行高normal / text/secondary |
| Payment | 11px / w600（设计可变字重590） / 行高normal / text/brand |

#### 方案 1（方案 E）· 无余额 · 空态 · 空态方案 1 只留入口（1802:2822）

已取得详细上下文；完整视觉与交互仍待校准。

| 已读显示文本（动态样例不作为默认值） | 文字属性原始读取 |
| --- | --- |
| Payments | 22px / w600（设计可变字重590） / 行高23px / text/primary |
| Send to an EZB account | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Free · Arrives instantly | 15px / w400 / 行高20px / text/secondary |
| Send to another bank | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| SWIFT · USD | 15px / w400 / 行高20px / text/secondary |
| Add a payee | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Save someone now, pay them later | 15px / w400 / 行高20px / text/secondary |
| Home | 11px / w500（设计可变字重510） / 行高normal / text/secondary |
| Payment | 11px / w600（设计可变字重590） / 行高normal / text/brand |

#### 方案 1（方案 E）· 转完第一笔（1802:2882）

已取得详细上下文；完整视觉与交互仍待校准。

| 已读显示文本（动态样例不作为默认值） | 文字属性原始读取 |
| --- | --- |
| Payments | 22px / w600（设计可变字重590） / 行高23px / text/primary |
| Send to an EZB account | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Free · Arrives instantly | 15px / w400 / 行高20px / text/secondary |
| Send to another bank | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| SWIFT · USD | 15px / w400 / 行高20px / text/secondary |
| Payees | 15px / w500（设计可变字重510） / 行高20px / text/secondary |
| AA | 15px / w600（设计可变字重590） / 行高20px / text/primary |
| Ahmed Ali | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Last sent $1,200.00 · 28 Sep | 15px / w400 / 行高20px / text/secondary |
| Home | 11px / w500（设计可变字重510） / 行高normal / text/secondary |
| Payment | 11px / w600（设计可变字重590） / 行高normal / text/brand |

#### 方案 1（方案 E）· 只收不付（1802:2958）

已取得详细上下文；完整视觉与交互仍待校准。

| 已读显示文本（动态样例不作为默认值） | 文字属性原始读取 |
| --- | --- |
| Payments | 22px / w600（设计可变字重590） / 行高23px / text/primary |
| Sending money is paused on this account | 17px / w600（设计可变字重590） / 行高23px / text/primary |
| You can still receive money. Open Help Centre to see why and what to do next. | 15px / w400 / 行高20px / text/secondary |
| Send to an EZB account | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Free · Arrives instantly | 15px / w400 / 行高20px / text/secondary |
| Send to another bank | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| SWIFT · USD | 15px / w400 / 行高20px / text/secondary |
| AA | 15px / w600（设计可变字重590） / 行高20px / text/primary |
| Ahmed Ali | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Last sent $1,200.00 · 28 Sep | 15px / w400 / 行高20px / text/secondary |
| AM | 15px / w600（设计可变字重590） / 行高20px / text/primary |
| AL MANSOORI TRADING | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| SWIFT · $8,500.00 · In progress | 15px / w400 / 行高20px / text/secondary |
| LT | 15px / w600（设计可变字重590） / 行高20px / text/primary |
| Lina Tan | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Last sent $450.00 · 20 Sep | 15px / w400 / 行高20px / text/secondary |
| Home | 11px / w500（设计可变字重510） / 行高normal / text/secondary |
| Payment | 11px / w600（设计可变字重590） / 行高normal / text/brand |

#### 方案 1（方案 E）· 一期 · 加卡后（1802:3122）

已取得详细上下文；完整视觉与交互仍待校准。

| 已读显示文本（动态样例不作为默认值） | 文字属性原始读取 |
| --- | --- |
| Payments | 22px / w600（设计可变字重590） / 行高23px / text/primary |
| Send to an EZB account | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Free · Arrives instantly | 15px / w400 / 行高20px / text/secondary |
| Send to another bank | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| SWIFT · USD | 15px / w400 / 行高20px / text/secondary |
| AA | 15px / w600（设计可变字重590） / 行高20px / text/primary |
| Ahmed Ali | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Last sent $1,200.00 · 28 Sep | 15px / w400 / 行高20px / text/secondary |
| AM | 15px / w600（设计可变字重590） / 行高20px / text/primary |
| AL MANSOORI TRADING | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| SWIFT · $8,500.00 · In progress | 15px / w400 / 行高20px / text/secondary |
| LT | 15px / w600（设计可变字重590） / 行高20px / text/primary |
| Lina Tan | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Last sent $450.00 · 20 Sep | 15px / w400 / 行高20px / text/secondary |
| Virtual card ···· 0192 | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Visa · Available $128,450.20 | 15px / w400 / 行高20px / text/secondary |
| Freeze card | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Turn it back on any time | 15px / w400 / 行高20px / text/secondary |
| Home | 11px / w500（设计可变字重510） / 行高normal / text/secondary |
| Payment | 11px / w600（设计可变字重590） / 行高normal / text/brand |


**本页仍需校准的业务边界：**

- 转入不自动保存是否为最终规则；T1最近转出／添加与T4最近往来的排序差异，星标内部顺序、相同时间及无交易联系人顺序如何定？（待校准）

## §2 首页状态

1. **空联系人：**保留顶部与两条转账入口，在原联系人区域展示 Add a payee 卡。卡片点击打开新增类型半框；标题、图标、辅助文字及内间距（待校准），不额外造空态插画或替换转账入口。
2. **只收不付：**两条付款入口禁用，禁用色引用本流程内的规格与规则；从联系人、详情再转等快捷入口同样不能绕过付款资格。联系人管理是否仍开放、限制原因文案和恢复方式（待校准）。
3. **首笔后与刷新：**同一对象仅占一行，至少一人即有 See all；转入不自动创建联系人。何时根据真实交易状态保存及排序（待校准）；当前 Mock 仅按明确完成且允许保存的快照保存。
4. **日历：**是否出现在最终首页（待校准）；没有定稿正文不扩张预约流程。

**逐元素与状态细则：**

| 状态 | 内容与可操作性 |
| --- | --- |
| 无联系人 | 两转账入口仍在；下方Add a payee卡进入T4类型选择；不出现空态插画卡／Send money替代入口 |
| 首笔转出后 | 联系人卡出现一行及See all；成功自动保存规则见T2／T3，不制造第二个人 |
| 有联系人 | 最多3条，可See all；同一联系人不重复占位 |
| 只收不付 | 两入口置灰；不允许进入付款链路。限制原因、解释文案、联系人再转／新增／日历的可用性（待校准） |
| 日历 | 设计注释称保留日历，但已读定稿图层隐藏且截图不显示；是否显示及预约正文范围（待校准） |
| 加卡后 | 已由用户确认纳入UI和交互，Cards区域完整显示，卡片、余额及状态全部Mock，见§3 |

切换Home与Payment复用现有底部导航能力；已开户宿主、未开户访问策略及Tab状态保存（待校准）。首页不复制账户流水，转入不作为“再转一笔”来源；我的收款信息留活期。

## §3 Cards 区域（已确认纳入）

1. **区域与排版：**Cards 与上方卡共用内容列。标题、行、副文和底部 Manage cards 按本流程标准行规格；卡片顶部、行间、底部及与 Payees 间距（待校准），未读到的 Cards 专属圆角／材质不从近似截图估值。
2. **图标与状态：**Virtual card 的卡片图形、Freeze card 的锁及两行尾随箭头精确资源／颜色（待校准）；Manage cards 使用 `textBrand`，文字具体字重和命中区域（待校准）。三项当前均仅展示，无可点击语义。
3. **数据与异常：**使用合成卡尾号、组织和可用金额；余额加载失败、无卡或冻结后的定稿状态（待校准），不新增未画状态、不接真实冻结接口。

**逐元素与状态细则：**

页面索引：FLOW T1 → T1-01 Payments 首页 →「方案1（方案E）· 一期 · 加卡后」（1802:3122）；用户本轮截图明确圈选本区域并确认显示。

1. Cards卡位于Payees卡下方，与首页其他卡片保持同一内容列；标题Cards，依次为Virtual card行、Freeze card行和Manage cards操作。与既有卡片复用同套表面、圆角和行组件；不根据截图像素估算额外尺寸。长页面向下可滚动，底部导航不遮挡Manage cards。
2. Virtual card ···· {尾号}：左钱包／卡片图形，右chevron；副文Visa · Available {可用金额}。卡号尾号、卡组织、余额全部来自合成Mock；示例0192和128,450.20不作为固定业务值。当前未提供对应定稿目的页／交互，仅展示该行，不绑定点击事件，不调用真实卡服务。
3. Freeze card：左锁图形，右chevron，副文Turn it back on any time。没有对应定稿的冻结确认、冻结后或解冻状态，仅展示该行，不绑定点击事件；不弹确认，不切换冻结状态，不新增Unfreeze card文案。
4. Manage cards：卡底居中的品牌色文字操作。保留设计中的文字与视觉样式；当前没有对应定稿目的页／交互，不绑定点击事件，不自行跳转旧卡管理页面或新增提示。
5. Cards内部文字、图标色和精确资产逐状态核对；不以卡片账户Mock为由绕过既有安全规则。卡片数据使用Mock；没有定稿交互时不模拟状态变化，不冻结真实卡、不请求真实余额。
