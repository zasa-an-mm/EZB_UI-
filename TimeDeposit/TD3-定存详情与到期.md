# TD3 · 定存详情与到期

> **状态：待逐页校准，可先开发。** 包含 App 详情、改名图标与到期处理、证明预览，以及对应 PDF 和公开验真网页。页面来源为[总览／我的定存](TD1-入口与总览.md)或[开立结果](TD2-开一笔定存.md)，提前取出见[TD4](TD4-提前取出.md)。基础导航、容器见[基础页面](../基础组件/基础页面.md)。

## §1 TD3-01 进行中详情

1. **页面与返回：**底 `bgBase`、正文左右16px，左玻璃返回回来源列表／结果；路由清栈细节（待校准）。详情为长页可滚动，不将1127px参考高度固定为运行高度，底部动作和系统安全区不遮最后一行。
2. **顶部摘要：**内容居中排列，56px圆形用途容器、内图26px；下为本金，设计36px / Bold / 行高44px / 字距−0.5，与正式普通字号档34px差异（待校准），不新增36字号。下为“{名称} · {存期}-month fixed deposit”，17px / Medium / 图中行高22px，与正式23px差异（待校准）。无名称时展示定存图标和存期。
3. **状态：**摘要各项间8px、底8px。Active 标签13px / Semibold / 图中行高17px，左右10px／上下4px、胶囊形、底 `feedbackSuccessBg`／字 `feedbackSuccess`；正式行高与组件映射（待校准）。主状态仅 Active／Closed，即将到期是 Active 子状态，不新增第三个顶层分段；Overdue 是仍归 Active 的异常展示。
4. **第一信息卡：**摘要下16px，Rate、Started、Matures on；依次显示年利率、起息日期、完整到期日期。卡宽随内容列、圆角20px、左右16px／上下4px、底 `bgGlass`、设计模糊13。
5. **第二信息卡：**上一卡下16px，At maturity、Interest at maturity、Deposit number；显示到期处理、到期利息、存单号。存单号尾随copy20px，独立点击区至少44px；复制反馈与敏感数据保护（待校准）。已计利息是否另列、实时更新时点（待校准），不能将到期利息当当前已计利息。
6. **信息行：**标签13px / Regular / 行高18px / `textTertiary`；下2px值17px / Medium / 行高23px / `textPrimary`，上下14px、最小高72px，行间1px `borderRow`。组件说明标签为 `textSecondary` 而实例为 `textTertiary`（待校准）；长值可换行、不截断存单号。
7. **动作卡：**再下16px，依次 Edit name and icon、Change what happens at maturity、Deposit certificate、Take out early。行最小高72px、上下8px、图文间12px；左40px容器内20px图形，主文17px / Medium / 行高23px，右chevron20px。确切业务图标及背景变体（待校准）。分别进§3、§4、§5、TD4。
8. **资格与错误：**加载／查询失败、存单不存在或归属失效、账户锁定时显示和返回（待校准）。只有服务端确认的本人存单可执行管理，不从界面按钮推断操作权限；主题／窗口变化不重复触发管理操作。

## §2 TD3-01a 即将到期

1. **摘要：**主状态保持 Active，标签“Active · Ends in {天数} days”。设计说明到期7天内出现提醒；天数边界、时区及当天显示（待校准），示例5天不是固定值。
2. **提醒：**摘要下展示“Renews on {到期日}”，说明“{本息} goes into a new {存期}-month deposit at that day's rate. You can change this until then.”；针对另外两种到期处理替换相应资金去向，不对所有人显示续存文案。提醒图形、表面、准确间距和其他两种完整文案（待校准）。
3. **信息顺序：**Rate、Matures on、At maturity、Interest at maturity、Started、Deposit number；设计与普通详情的日期顺序不同，保留本状态顺序。字体与卡片规格同§1，不以参考938px裁切内容。
4. **修改截止：**到期当天之前允许改到期处理；说明“until then”与“到期当天之前”的准确截止时间（待校准），不自行延长到当日末。操作入口是否全部沿用普通详情及禁用解释（待校准）。

## §3 TD3-01c 编辑名称与图标

1. **半框：**原详情上开半框，标题 Edit name and icon，说明 Only you see this. Your deposit doesn't change.；标题22px / Semibold，图中行高27px与正式28差异（待校准）；说明15px / Regular / 行高20px，标题下8px。底色、圆角、初始高度和外点／下滑规则（待校准）；矮窗口最高90%，内容可滚动。
2. **输入：**Name 标准字段，带当前名称；标签13px / Regular / 行高18px、值17px / Medium / 行高23px，底 `bgField`、圆角16px、左右16px。名称为空、长度、字符、重名和多语言（待校准）。名称是显示别名，不修改开户户名、利率、本金或存单号。
3. **图标：**与 TD2 用途同一八项：Travel／Home／Education／Car／Family／Gift／Rainy day／Just grow，两行四列、圆56px／内图24px，标签13/18、间8px；当前图标选中，变更选中表面（待校准）。
4. **Save：**品牌主按钮56px、圆角28px、17px / Semibold / 行高23px；保存后回详情，同一对象在首页摘要、主页和列表同步展示。取消不应静默保存未确认修改；提交时点、失败保留、重试和并发覆盖（待校准）。此处选填编辑不自动要求系统键盘弹出，点 Name 再编辑；关闭时键盘和焦点恢复（待校准）。

## §4 TD3-02 修改已开存单的到期处理

1. **入口与选项：**详情动作打开 When it matures，同[开立时的三选一半框](TD2-开一笔定存.md)，当前真实指令预选。三项名称、金额去向与视效按该屏描述，仍保留选项配色冲突标记。
2. **认证：**选择后 Face ID 确认、PIN 兜底；这是修改已开存单指令，与开立前仅编辑本地选择不同。认证成功且业务修改成功才更新真实指令；取消和失败不显示已保存。具体成功反馈、失败／处理中状态与关闭时点（待校准）。
3. **截止与并发：**到期当天之前允许改；具体时区、截止时刻、重复点击、同时发生到期与修改时的返回（待校准）。已结清／逾期是否禁止及错误说明（待校准），不能只隐藏按钮却信任旧页面权限。
4. **返回：**取消半框回原详情，保持普通滚动位置；外点／下滑、认证取消后的回显和旧值恢复（待校准）。不把未返回确认的选择当服务端已生效。

## §5 TD3-03 存款证明 · App 预览

1. **页面：**标题 Deposit certificate，左返回回来源详情，底 `bgBase`；标题样式与基础导航内置标题的最终组合（待校准），不复制一个重复标题。正文左右16px，PDF预览与验真提示上下排列，底部 Share PDF／Save to Files 独立固定。
2. **PDF：**文件由后台生成，App 展示真实 PDF，不用前端根据字段重画证明。预览按原页比例缩放，保持白纸打印配色；缩放、翻页控件、下载失败、过期 URL、加载中与重试（待校准）。参考稿预览只是缩略，不能把缩略后的3px文字当PDF正式字号。
3. **验真提示：**预览下12px，圆角16px、内边距16px、`bgGlass`；左shield20px、图文间12px。标题 Anyone can check it’s genuine，实例17px / Semibold / 行高23px；说明15px / Regular / 行高20px，下4px，包含本人本证明编号与验证码及 ezb.com/verify。Reminder组件描述标题15与实例17差异（待校准）。链接可点，带参数打开§7结果页；二维码同一个带参链接。
4. **底部操作：**底栏上16px、左右16px、按钮间8px、底部8px再加实时安全区。Share PDF 品牌实底，Save to Files 品牌文字；都最小高56px、圆角28px、17px / Semibold / 行高23px。分别调系统分享／文件保存，取消返回预览，不视为失败；失败反馈与文件名（待校准）。不要将设计中的Home Indicator当按钮区固定26px安全区。
5. **可用范围：**Active 与 Closed 均可开证明；资料权限、生成时点、语言选择、生成后是否缓存和敏感文件清理（待校准）。当前证明下载不等于验真服务已经存在，不在文档里虚构接口协议。

## §6 TD3-03 存款证明 PDF 模板

> 此节为服务端 PDF 的打印版式，不是 App 页面样式。模板版本包含进行中、到期结清、提前取出结清、极限长户名／大金额／长账号。

1. **纸张：**A4竖版210×297mm，595×842pt、固定1页。左右页边距36pt，上33pt，内容宽523pt；页脚文字顶端距底边30pt，验真与签章块固定在页脚上方27pt。原画布794×1123px，设计注明1px=0.75pt；纸张整数舍入差异（待校准），不把画布像素当App布局值。
2. **字体：**Inter Regular／Medium／SemiBold／Bold 嵌入 PDF。阿拉伯语后续版本字体和版式（待校准），不声称本版已支持。标题15pt Bold；户名10pt SemiBold；版块标题9pt Bold全大写、字距6%；小标签6.5pt SemiBold全大写、字距6%；字段名／值7.5pt、值Medium、本金Bold；说明7.5pt／行高11pt；页眉信息7.5pt，验真说明7pt，页脚6.5pt。未注明行高者（待校准），不自行换算。
3. **颜色：**打印主文字#0C1B26、次文字#5B6B80、辅助#8A97A8、分隔线#E4E9F0；Logo水印4%不透明度。这些为PDF发布版式，不能借用于App私有颜色。
4. **页眉：**左上Logo占位高30pt，正式Logo（待校准）；右侧DEPOSIT CERTIFICATE、Fixed deposit、存单号和开具时间／语言，具体对齐及中间留白按模板，未取得参数（待校准）。Logo水印居中高112pt、4%不透明度。
5. **户名与说明：**说明句随Active／到期结清／提前取出变化，不把已结清描述为仍持有；准确三种法律文案（待校准）。ACCOUNT HOLDER下为户名，最多2行，超出省略号；公开验真页另做掩码，PDF本人户名的正式隐私规则（待校准）。
6. **字段表：**DEPOSIT DETAILS，下附 Amounts in USD；从上到下 Deposit no.、Start date、Maturity date、Interest rate、Principal、Funding account、Status。字段名列135pt，值列自适应，单行内边距上下8pt／左右9pt，1pt描边、圆角4.5pt。户名加此七字段为限定资料，不添加主账号序号、账户类型、凭证类型／号码、产品代码、支取方式或通存通兑标志等内部字段。
7. **三种状态：**进行中、已结清到期、已结清提前取出；字段相同，只更换说明句、状态行和开具时间。已结清仍可开证明，验真应说明真实但存单已结清；状态精确大小写与到期字段是否保留原计划日期（待校准）。
8. **格式与极限：**金额千分位、两位小数、不带货币符号；预留999,999,999,999.99宽度。日期如13 Oct 2026，开具时间银行时区，利率4.50% p.a.；活期账号按IBAN四位分组。存单号、账号、验证码不截断不换行。超过模板支持长度时的正式处理（待校准），不得静默裁掉关键账号。
9. **验真块：**二维码63×63pt，链接`ezb.com/verify?no=…&code=…`，扫码直达结果；编号与8位验证码配对，验证码显示XXXX-XXXX，由后台生成。模板里的名称“证明编号／存单号”目前混用，真实凭证编号是否独立于存单号、重开是否产生新凭证（待校准），不能擅定接口字段含义。
10. **电子章：**右下角78pt直径电子章位，配签名线与Authorised signatory, EZB。正式电子章由行方提供（待校准）；虚线圈与BANK STAMP只作占位，正式PDF不出现。页脚银行法定名称、持牌信息由法务提供（待校准），页码Page 1 of 1，不发布占位法律文本。

## §7 TD3-03b 验真网页 · 输入

1. **使用者与入口：**供第三方手机浏览器查看，无需登录。App链接与PDF二维码带编号和验证码直接展示结果；手动访问显示输入页。浏览器地址栏和系统状态栏是设备UI，不在网页内复制。
2. **页首与标题：**Logo＋Certificate check。标题 Check a deposit certificate，设计24px／Bold、行高未注明；网页是否沿用App正式22/28（待校准），不自动套用。说明 Enter the certificate no. and code printed at the bottom of the certificate.，15px / Regular，行高（待校准）。正文左右16px，背景 `bgBase`、文字 `textPrimary`／`textSecondary`，浅色网页和桌面宽度（待校准）。
3. **两个字段：**Certificate no.、Verification code，采用标准字段的标签13/18、值17/23、圆角16px、`bgField`，左右16px；上下内边距、字段间距、焦点和错误态（待校准）。初始为空，设计示例不是默认真实值。验证码显示XXXX-XXXX，允许字符、大小写与分隔符规范化（待校准）。
4. **Check：**品牌主按钮、最小高56px、圆角28px、17px / Semibold / 行高23px；底部说明 Got a QR code? Scan it with your phone camera to skip this step.，13px / Regular，行高／间距（待校准）。必填输入时聚焦首个字段，网页端自动弹键盘受浏览器能力限制，不强造系统键盘。
5. **验证：**编号与验证码共同有效才出摘要；空值／格式错、请求中、网络失败和带参失败回退（待校准）。不在日志记录验真凭据，不因缺一个参数直接展示其他人的证明摘要。

## §8 TD3-03b 验真网页 · 真实／已结清／不匹配

1. **真实：**成功图形circle-check，标题 This certificate is genuine，下方Certificate {编号} · issued {开具日期}。图形参考圆盘约64.48px／内图29.76px，正式规格（待校准）；标题24px与正式档位差异同§7。
2. **摘要卡：**顶部说明下20px，圆角20px、左右16px／上下4px、`bgGlass`；Account holder（打码户名）、Amount（币种金额＋存期＋年利率）、Dates（起止日）、Status today（当前状态）。行标签13/18 `textTertiary`、值17/23 `textPrimary`、行最小72px／上下14px，标签色与组件说明差异（待校准）。只展示摘要，不显示活期余额或完整户名；掩码算法（待校准）。
3. **核对提示：**卡下12px，“Make sure these match the certificate you were given. We never show balances or full names here.”，13px / Regular / `textTertiary`，行高（待校准）。
4. **真实但已结束：**仍显示 genuine；黄色警示 This deposit has ended，说明到期或提前取出日期及The money is no longer in a fixed deposit.；Status today 为对应Closed子状态。警示表面、图标与两种结清完整文案（待校准）。不是把旧证明判为伪造，也不能让旧证明看起来资金仍在定存。
5. **查不到：**We can’t match this certificate；说明Check the certificate no. and code and try again. If it still doesn’t match, the certificate may not be genuine.。Try again回输入，Contact EZB目标（待校准）；不区分编号错或验证码错。原字段保留及重新聚焦规则（待校准）。
6. **频控：**图上After 5 wrong tries in an hour, checks are paused for 1 hour.；设计注释明确数字示意，最终次数、窗口、限制范围、恢复和暂停状态视觉（待校准），不能作为已确认风控策略。
7. **资料时点：**证明真实性与当前存单状态分开；到期／提前取出后验证仍查当前状态。缓存有效期、撤销凭证、逾期状态与服务异常（待校准），不能将查询失败当不真实。

## §9 TD3-01b／e 已结清详情

1. **共通摘要：**顶部金额为结清本息或退回本金，名称下显示Closed · Matured或Closed · Taken out early；颜色、图形与Active区分（待校准）。已结清只留Deposit certificate动作，不显示修改指令、编辑、提前取出。
2. **到期回活期：**Started、Matured on、Paid to current account、Rate、Interest earned、Deposit number；资金去向明确金额，不只写“已到期”。顶额为本息，信息行与§1同规格。
3. **本息续存：**Started、Matured on、Renewed（本息合计）、Rate、Interest earned、Deposit number、New deposit（新存单号）。旧单属于Closed，新单独立Active；New deposit是否可点及跳转（待校准）。
4. **本金续存：**同上，Renewed显示本金，另行Paid to current account显示利息，再有新存单号。不能把本金与利息都写进续存金额。
5. **提前取出：**Started、Taken out early on、Paid to current account、Rate、Interest earned（0）、Deposit number；保留历史合同利率但不表示支付利息。列表以实际结清日期排序，顶部金额与已回活期数一致。
6. **异常：**钱款处理未完成时是否进入Closed、利息调整、信息更正与证明生成时点（待校准），不拿预期金额覆盖真实处理结果。

## §10 TD3-01f／g 到期未转回 · Overdue

1. **触发：**到期指令需回活期的款项因本人活期冻结、只付不收等无法入账时，存单显示Overdue · not paid out，黄色状态，仍归Active并置顶。本息续存不受活期状态影响，不因此逾期；本金续存但利息无法入账时的部分成功与本金去向（待校准）。
2. **摘要与字段：**顶额为待转金额，下面存期与状态。信息为Rate、Started、Matured on、Waiting to go to（本人USD活期尾号）、Interest earned、Deposit number；是否另展示逾期利息和应转总额拆分（待校准）。状态色用正式警示语义，精确token、标签与提示卡样式（待校准）。
3. **活期仍受限：**提醒We couldn’t pay this out，说明到期但活期目前不能收款，钱保留在此；Move to current account禁用，下方Available once your account is back to normal，Contact us与Deposit certificate可见。联系客服落点（待校准）；App无强制处置功能。
4. **活期已恢复：**提醒Move your money to your current account，说明不会自动再转，用户点Move {待转金额} to current account手动操作；验证同提前取出。授权、提交、处理中／未知／失败／成功后的落点和状态（待校准），不因入口已可点就自动转账。
5. **逾期利息：**注释写“按活期利率计息（现为0）”，受限画面写“with no extra interest”；动态利率变化时文案与金额规则（待校准），不固定假定永远0。
6. **长期未处理：**设计说明满6个月按监管要求强制处理；真实期限、计算口径、运营流程和客户说明（待校准）。本契约只记录设计要求，不把它当已核实法规或在App实现强制操作。

## §11 TD3-04 续存后的新存单

1. **状态与编号：**续存创建一笔新存单，状态Active；不新增Renewed主状态。本金为实际续入金额，年利率采用续存当天该存期利率，不沿用旧利率。
2. **字段：**Rate、Started、Renewed from（旧存单号）、Matures on、At maturity、Interest at maturity、Deposit number。Renewed from放Started之后，信息卡行视觉同§1；点击旧号导航（待校准）。
3. **旧单：**进入Closed，并写清Renewed金额与New deposit新号，本金续存另写回活期利息。新旧存单互相关联，不覆盖旧历史。
4. **到账记录：**转回活期时新增“定存到期”交易；流水详情、通知与记账时点（待校准）。用途名称／图标是否继承、续存产品停售或失败的处理（待校准）。
