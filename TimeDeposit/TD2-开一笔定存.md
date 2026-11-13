# TD2 · 开一笔定存

> **状态：待逐页校准，可先开发。** 主路径为[主页](TD1-入口与总览.md)→金额→复核→认证→结果，选存期、用途与到期处理均为页内半框。页面使用[基础容器](../基础组件/EzbScaffold.md)与[导航](../基础组件/EzbAppBar.md)，不把参考整页选期变成必经步骤。

## §1 TD2-02 金额与试算 · 正常

1. **页面与返回：**底 `bgBase`，正文左右16px；标题 How much to put in?，设计28px / Bold / 行高33px / `textPrimary`，正式页面标题22/28差异（待校准）。左返回回定存主页；金额、用途与存期返回后的保留（待校准），不继承 KYC 清空规则。内容可滚动，底部 Continue 在键盘上方且避让实时系统安全区。
2. **初始值与焦点：**主页金额原样预填、数字全选，进入自动聚焦并弹系统小数键盘，直接打字覆盖；存期和用途同步带入。未选用途显示 Add · Optional。不重新给用户默认金额或换成可用余额；冷启动恢复与参数失效（待校准）。
3. **金额字段：**标题下间距（待校准），字段左右16px、上下14px，符号与数值间4px；金额34px / Bold / 行高40px，符号 `textSecondary`、数值 `textPrimary`。图中圆角14px与正式16px差异（待校准），不另造 token。正常底 `bgField`，聚焦边框和选区颜色的精确变体（待校准）。输入精度、最大位数、前导零和货币格式（待校准）。
4. **余额与起存额：**金额下8px，“Available {可用余额} · Minimum {起存额}”，13px / Regular / 行高18px / `textSecondary`。固定本人 USD 活期为资金来源，正式起存额、余额口径和单笔上限（待校准）。主页试算可超余额，本页进入即校验。
5. **可编辑行：**Term、Saving for、At maturity 从上到下排列。标签15px / Regular / 行高20px / `textSecondary`，右值15px / Semibold / 行高20px / `textPrimary`，末尾 chevron-right20px；行高度与上下间距（待校准）。Term 显示“{存期} · {年利率}”，Saving for 显示用途名或 Add · Optional，At maturity 默认 Renew with interest。分别打开§3、§5、§4半框，关闭回原页。
6. **收益摘要：**Interest at maturity → 到期利息；Back on {到期日} → 本息合计，左右对齐、标签15px / Regular / 行高20px，值15px / Semibold / 行高20px。试算取当前金额与存期；利率、到期日、本息、计息日历与舍入以最终业务数据为准（待校准），未确认前只可用明确合成场景，不默认生产公式。
7. **Continue：**宽度铺满内容列、最小高56px、圆角28px、17px / Semibold / 行高23px；正常 `brandPrimary`／`textOnBrand`，禁用 `bgDisabled`／`textDisabled`。有效金额与有效试算才能进复核，试算中／失败／过期对按钮的完整矩阵（待校准）；不再放快捷金额芯片。
8. **适配：**支持310px宽、200%字号，标签值空间不足时换行；正文不被键盘／固定底栏覆盖。重建、刷新、切主题不反复弹键盘或把输入恢复成示例。

## §2 TD2-02a／b 金额异常

| 状态 | 文案与操作 | 保留与阻断 |
| --- | --- | --- |
| 低于起存额 | The minimum is {起存额}. | 原样保留金额，错误就近显示，Continue 禁用 |
| 超过余额 | More than your available {余额}.；后接 Use {余额} | 不悄悄改金额；点 Use 才填入当前可用余额并重算，Continue 在有效前禁用 |
| 可用余额低于起存额 | 补救操作改 Add money | 目标页、返回刷新与准确说明（待校准），不新增充值正文 |
| 超过单笔上限 | 本页校验，不在主页报错 | 精确文案、校验优先级、展示上限与补救（待校准） |
| 空／零／格式非法 | 不允许提交 | 错误触发时点、文案、小数规则（待校准） |

错误辅助文本13px / Regular / 行高18px / `feedbackError`，Use 使用可点品牌文字；错误背景、边框及补救文字间距（待校准）。余额变化、多个错误同时存在时的优先顺序（待校准）。改金额保留已选存期、用途与到期处理，试算响应不得把旧金额结果回填到新输入；具体更新时点（待校准）。

## §3 TD2-01 选存期半框

1. **入口与结构：**金额页 Term 行打开，遮罩覆盖原页，标题 Choose a term，说明 The rate is fixed for the whole term.；不新建整页。标题22px / Semibold，图中行高27px与正式28px差异（待校准）；说明15px / Regular / 行高20px / `textSecondary`，标题下8px，选项前20px。
2. **列表：**只列可售且一年以内存期，例1／3／6／12个月；标题“{存期} · {年利率} a year”，17px / Medium / 行高23px，副文“Ends {到期日}”，15px / Regular / 行高20px。选中标记、选项表面与间距（待校准），不将产品档数或示例利率硬编码为正式政策。
3. **选择：**带入当前存期，选择即关闭、回填并重算。下架产品、切期后金额不符合起存额、利率变化、无可售存期（待校准）。取消／系统返回／外点／下滑均不应静默切成另一存期，具体关闭行为（待校准）。
4. **尺寸与安全区：**最大内容列560px、矮窗口最高90%，列表内部滚动；背景、顶部圆角、拖拽指示与初始高度（待校准），不得被键盘或系统栏遮挡。

## §4 TD2-03 到期处理半框

1. **入口：**金额页和复核页的 At maturity，标题 When it matures；说明 You can change this any time before it matures.。标题22px / Semibold / 图中行高27px（正式28px差异待校准），说明15px / Regular / 行高20px；标题下8px、说明下20px。
2. **三选一：**默认 Renew with interest · Recommended；另外 Renew, pay interest out 与 Pay it all out。三项只回本人 USD 活期，不提供选择他人或其他币种账户。

| 选项 | 动态说明含义 | 图形 |
| --- | --- | --- |
| Renew with interest · Recommended | 本息合计进入新一笔同存期定存，采用到期当天该存期利率 | percent22px |
| Renew, pay interest out | 本金续存，利息回本人 USD 活期 | wallet22px |
| Pay it all out | 本息合计回本人 USD 活期 | undo-2 22px |

3. **选项视觉：**圆角16px、内边距16px、图文间14px、选项间8px；标题17px / Medium / 行高23px，副文15px / Regular / 行高20px。当前实例选中 `bgBrandSelected`、22px实心品牌圆勾内14pxcheck；未选 `bgSurfaceRaised`、22px控件圈。组件描述另写 `bgSurfaceHover`／`bgBrandSubtle`，且副文实例有 `textTertiary`、描述为 `textSecondary`，最终选项变体（待校准），不自行二选一。
4. **回填：**开立前选择即收起，金额／复核上的 At maturity 即时更新；本阶段不单独执行已开存单的修改认证。取消、外点、下滑的保留行为（待校准）。到期当天更改截止点、产品停售的续存处理与利率来源（待校准）。

## §5 TD2-03a 用途半框

1. **标题与说明：**What are you saving for?，22px / Semibold / 图中行高27px；下方 Optional. You can change the name and icon any time.，15px / Regular / 行高20px / `textSecondary`，标题与说明间8px；其余上下间距（待校准）。用途选填，不改变底层标准定期产品。
2. **Name 字段：**标签 Name、当前名称值；标签13px / Regular / 行高18px、值17px / Medium / 行高23px；底 `bgField`、圆角16px、左右16px，字段上下与焦点变体（待校准）。长度、空值、emoji／多语言、默认回退名称（待校准）。本页无必填可编辑项，是否点击 Name 才弹键盘按最终交互校准，不因 Name 存在自动认定必填。
3. **八个图标：**Travel／Home／Education／Car／Family／Gift／Rainy day／Just grow，分别 plane／house／graduation-cap／car／baby／gift／umbrella／trending-up；两行四列，图形24px置于56px圆形内，图标到标签8px；标签13px / Regular / 行高18px。未选圆底 `bgField`，选中底色、图标前景和选中默认项（待校准）。
4. **Done：**品牌主按钮，最小高56px、圆角28px、17px / Semibold / 行高23px。确认后回原页带名称和图标；取消／关闭是否丢弃草稿（待校准），不擅自改成自动保存。

## §6 TD2-04 复核与认证

1. **页面：**标题 Check and confirm，底 `bgBase`、正文左右16px，返回金额页；设计标题28/33与正式22/28差异（待校准）。长正文滚动，底部认证操作独立且不遮挡条款。
2. **锁定提醒卡：**标题 Your money is locked for {存期}，17px / Semibold / 行高23px / `textPrimary`；副文 Need it early? You get your {本金} back, but no interest.，15px / Regular / 行高20px / `textSecondary`。卡圆角16px、内边距16px、左shield20px、图文间12px、标题说明间4px、底 `bgGlass`，提醒卡组件描述“标题15”与实例17的差异（待校准）。
3. **信息卡：**提醒下16px；卡圆角20px、左右16px／上下4px、`bgGlass`。从上到下 Deposit（存期＋年利率）、Saving for（已选名称）、From（本人 USD 活期＋尾号）；未设用途是否隐藏该行（待校准）。From 只读，无箭头、不允许换账户。
4. **第二卡：**上张卡下16px，依次 At maturity、Starts、Matures on。At maturity 右chevron20px，整行点击原地弹§4半框并即时更新，不跳金额页、不使用旧pencil。其余只读。
5. **信息行样式：**标签13px / Regular / 行高18px / `textTertiary`，下2px为值17px / Medium / 行高23px / `textPrimary`；最小高72px、上下14px，行间1px `borderRow`分隔。标签色与 Info Row 描述的 `textSecondary` 差异（待校准）。长账号／文案可换行，不截断关键值。
6. **合计卡：**再下16px，You put in／Interest／You'll get back，标签15px / Regular / 行高20px / `textSecondary`，前两值15px / Semibold / 行高20px，合计17px / Semibold / 行高23px / `textPrimary`。不显示利息税行；这是设计的产品呈现，不在此推导税务法规。金额与日期必须和当前试算一致。
7. **条款：**卡下说明 The rate is fixed for the whole term. By confirming, you agree to the Fixed Deposit terms.，13px / Regular / 行高18px / `textSecondary`；条款链接范围、目标、语言／版本与打开失败（待校准）。没有独立勾选框定稿，不额外新增。
8. **确认按钮：**Confirm with Face ID，图标随真实能力，品牌主按钮56px／圆角28px／17px Semibold／23行高；PIN 兜底继续用安全键盘。具体PIN文案、失败次数、锁定、取消、因子升级与提交中返回（待校准）；不直接把 Payment 全部策略视作定存政策。
9. **加载与防重：**组件 loading 设计为20px spinner 替换文字与图标、按钮宽和底色保持、不叠外部遮罩。当前开立是否采用该局部态、超时阈值（待校准）；不得重复确认创建两笔。试算／利率过期时的重新复核（待校准），未知结果不得重发开立。

## §7 TD2-05 四类结果

1. **排版：**状态图形、标题、说明、底部主次按钮；图形圆盘104px／内图约48px，正式资源、图形颜色和间距（待校准）。标题按正式22/28，设计结果标题的完整字重和差异（待校准）；说明15px / Regular / 行高20px / `textSecondary`，长金额和日期可换行，正文不固定高。

| 状态 | 标题与说明 | 操作 |
| --- | --- | --- |
| opened | Your {本金} is now saving；It earns {年利率} a year until {到期日}. We'll remind you a week before it matures. | Done、View deposit |
| opening | We're opening your deposit；This usually takes a few minutes. Your {本金} is on hold until then, and we'll let you know when it's done. | Done、View deposit |
| not opened | Deposit not opened；We couldn't open this deposit. No money has left your account. | Back to Fixed deposits、Go to Help Centre |
| no answer yet | We're still confirming；Your connection dropped before we heard back. Please don't try again — check Fixed deposits in a minute. | View Fixed deposits |

2. **落点与事实：**View deposit 指向本次存单，View Fixed deposits／Back to Fixed deposits 回主页；Done 的准确清栈落点（待校准）。处理中不假装已开立，未知仅查询原请求；处理中详情无正式存单号时的展示（待校准）。失败不披露底层敏感原因，Help Centre 目的页（待校准）。
3. **资金与通知：**成功、在途冻结、失败释放与余额更新应匹配服务端事实；轮询、后台通知、到期前一周提醒渠道与可配置时点（待校准）。不能将本地计时当开立成功，也不能用 UI Mock 宣称真实资金已冻结／释放。
4. **生命周期：**认证取消、离开复核、退出开立、切后台、重启、身份改变后的输入保留／撤销和恢复位置（待校准）。PIN与认证证明不持久化、不写日志，已提交结果不能因返回又开一笔。
