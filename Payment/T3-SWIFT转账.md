# T3 · SWIFT 转账

> **状态：待校准，可先开发；真实接口联调完成后统一校准。** 本流程视觉规格见本流程内的视觉规格与逐屏规则，状态登记见各页下方的状态文案与属性。T3外框旧名“新增SWIFT收款人”不代表本流程只做新增。

## 本流程视觉规格（待校准项就地标注）


1. **页面与导航：**普通表单和详情复用基础页面，背景 `bgBase`；正文左右16px，宽窗口最大560px。返回、关闭、系统返回及返回手势遵循本屏业务返回规则；未明确落点时标“（待校准）”，不自动套用 KYC 清空规则。正文标题22px / w700 / 行高28px / `textPrimary`；标题相对导航点击区域的垂直距离（待校准）。有副说明时使用15px / w400 / 行高20px / `textSecondary`；标题与副说明、首个内容的间距未单独列明者（待校准）。
2. **表单：**标准输入底 `bgField`、圆角16px、左右16px、上下14px；标签13px / w400 / 行高18px / `textSecondary`，下2px为值17px / w500 / 行高23px / `textPrimary`，占位 `textTertiary`。文字自撑高，最小高度（待校准）。聚焦2px `borderFocus`，标签 `textBrand`；错误辅助文案13px / w400 / 行高18px / `feedbackError`，与字段间距、错误背景及边框转换（待校准）。禁用 `bgDisabled`／`textDisabled`；只读保留正常文字颜色，不伪装成不可辨认的禁用态。未取得字段间距时逐屏标注，不默认照搬 KYC。
3. **金额：**当前开发采用正式34px / w700 / 行高40px、圆角16px；输入左右16px、上下14px，符号与金额间4px；符号 `textSecondary`，金额 `textPrimary`。设计曾为圆角14px，最终视觉匹配（待校准），不新增正式 token。余额／额度说明13px / w400 / 行高18px / `textSecondary`，距金额8px。
4. **主次操作：**主按钮最小高56px、圆角28px、文字17px / w600 / 行高23px；正常 `brandPrimary`／`textOnBrand`，禁用 `bgDisabled`／`textDisabled`。文字换行可增高，处理中阻止重复触发并播报状态；按下态复用正式按钮状态。次操作的具体表面、危险按钮颜色和相邻间距未明确者（待校准），不猜值。固定底部操作区与正文共用内容列，底部消费实时安全区；区域上下内边距（待校准）。
5. **半框：**背景表面语义、顶部圆角、标题到内容间距（待校准）；标题22px / w700 / 行高28px / `textPrimary`。宽窗口最大560px，矮窗口限高90%，内容内部滚动；操作和固定 Other 不被滚动区或系统栏遮挡。外点、下滑、系统返回是否关闭依各屏规则，未明确者（待校准）。
6. **行、详情与空态：**标准行最小高72px，上下8px；左40px图形容器、图形20px，与文字间12px。主文17px / w500 / 行高23px / `textPrimary`，副文15px / w400 / 行高20px / `textSecondary`，尾随箭头20px；头像字母15px / w600 / 行高20px。详情字段标签和值的布局、分隔线及行距未取得者（待校准），不能仅因复用组件省略差异。空态标题22px / w700 / 行高28px，说明15px / w400 / 行高20px；插画、对齐和间距依各屏，缺项（待校准）。
7. **适配与可访问性：**同名语义 token 分别映射明暗主题。支持100%／200%字号，长文自然换行；图标装饰不重复朗读，交互图标须有可读名称，独立点击区至少44px。310px窗口可用，安全区和键盘分别避让，底部导航、PIN删除键和主要操作不得被系统栏遮挡。


## §1 T3-01 银行信息

1. **页面与元素：**返回来源 Payment，标题 Their bank details、副说明、Country、国家相关账户字段、SWIFT／BIC、风险提示、Continue，公共视觉见下述本流程视觉规格；各字段间距及说明到字段间距（待校准）。初始仅 Country，不自动弹输入法。
2. **国家半框：**可搜索国家列表，国家名与所需资料副文用本流程标准行规格；搜索占位、排序、无结果及禁用国家文案（待校准）。选国家后首个可编辑必填字段聚焦时机（待校准）；初次仅选择器不抢键盘。
3. **银行输入：**账号／IBAN／ABA 按国家配置显示；SWIFT 手输，查询后银行名与城市只读回显，回显字号／图标（待校准）。查不到、格式错误、不支持国家逐字段报错，正式验证和文案（待校准）。
4. **既有联系人：**选择后仅回填银行资料，Continue 仍经过收款人页。国家变更的当前 Mock 处理为清依赖银行与地址、废弃旧报价，保留无关金额／用途／Reference；真实字段依赖（待校准）。

**逐元素与状态细则：**

1. 标题Their bank details，说明We send in US dollars by SWIFT.；初始只有Country／Choose a country，不预填国家或示例账号。提示Check these with your recipient／Money sent to a wrong account may be hard to get back.。
2. 选国家后按配置显示账户字段：IBAN国家为IBAN，其他国家账号，美国加9位ABA；加拿大transit／institution列为配置需求，完整国家字段和支持范围待提供，不能从示例补全世界规则。SWIFT／BIC保持手输，查到后回显银行名·城市；银行小图标为示意、可行性和资源（待校准）。
3. 国家选择为可搜索半框，行副标题说明所需字段。无支持国家报Country错误、隐藏下面字段、Continue禁用。IBAN格式错、SWIFT查不到保留输入并就近提示；准确格式规则和错误文案按校准清单及（待校准）项。
4. 账号字段右侧选既有海外联系人，半框规则复用T2；选中回本页，国家、账号／IBAN和SWIFT回填只读，Continue进入T3-02，姓名／地址回填只读，再Continue到金额。不按早期说明跳过收款人页。


### T3-01 银行信息（国家 + 账户） · 状态文案与属性（待校准）


#### EZB · 默认（空）· 先选国家（1959:4572）

已取得详细上下文；完整视觉与交互仍待校准。

| 已读显示文本（动态样例不作为默认值） | 文字属性原始读取 |
| --- | --- |
| Their bank details | 28px / w700 / 行高33px / text/primary |
| We send in US dollars by SWIFT. | 15px / w400 / 行高20px / text/secondary |
| Country | 13px / w400 / 行高18px / text/tertiary |
| Choose a country | 17px / w500（设计可变字重510） / 行高23px / text/disabled |
| Check these with your recipient | 17px / w600（设计可变字重590） / 行高23px / text/primary |
| Money sent to a wrong account may be hard to get back. | 15px / w400 / 行高20px / text/secondary |
| Continue | 17px / w600（设计可变字重590） / 行高23px / text/disabled |

#### EZB · 填好（IBAN 国家）（1754:3904）

已取得详细上下文；完整视觉与交互仍待校准。

| 已读显示文本（动态样例不作为默认值） | 文字属性原始读取 |
| --- | --- |
| Their bank details | 28px / w700 / 行高33px / text/primary |
| We send in US dollars by SWIFT. | 15px / w400 / 行高20px / text/secondary |
| Country | 13px / w400 / 行高18px / text/tertiary |
| United Arab Emirates | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| IBAN | 13px / w400 / 行高18px / text/tertiary |
| AE07 0331 2345 6789 0123 456 | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| 23 characters, starts with AE | 13px / w400 / 行高18px / text/tertiary |
| SWIFT / BIC code | 13px / w400 / 行高18px / text/tertiary |
| EBILAEAD | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Emirates NBD · Dubai | 13px / w400 / 行高18px / text/tertiary |
| Check these with your recipient | 17px / w600（设计可变字重590） / 行高23px / text/primary |
| Money sent to a wrong account may be hard to get back. | 15px / w400 / 行高20px / text/secondary |
| Continue | 17px / w600（设计可变字重590） / 行高23px / text/on-brand |

#### EZB · 选收款人（快捷入口）（1838:2830）

已取得详细上下文；完整视觉与交互仍待校准。

| 已读显示文本（动态样例不作为默认值） | 文字属性原始读取 |
| --- | --- |
| Their bank details | 28px / w700 / 行高33px / text/primary |
| We send in US dollars by SWIFT. | 15px / w400 / 行高20px / text/secondary |
| Country | 13px / w400 / 行高18px / text/tertiary |
| United Arab Emirates | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| IBAN | 13px / w400 / 行高18px / text/tertiary |
| AE07 0331 2345 6789 0123 456 | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| 23 characters, starts with AE | 13px / w400 / 行高18px / text/tertiary |
| SWIFT / BIC code | 13px / w400 / 行高18px / text/tertiary |
| EBILAEAD | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Emirates NBD · Dubai | 13px / w400 / 行高18px / text/tertiary |
| Check these with your recipient | 17px / w600（设计可变字重590） / 行高23px / text/primary |
| Money sent to a wrong account may be hard to get back. | 15px / w400 / 行高20px / text/secondary |
| Continue | 17px / w600（设计可变字重590） / 行高23px / text/on-brand |
| Your payees | 22px / w600（设计可变字重590） / 行高28px / text/primary |
| AM | 15px / w600（设计可变字重590） / 行高20px / text/brand |
| AL MANSOORI TRADING LLC | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Emirates NBD ···· 3456 | 15px / w400 / 行高20px / text/secondary |
| BS | 15px / w600（设计可变字重590） / 行高20px / text/brand |
| BRIGHTLINE SUPPLY INC | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Bank of America ···· 2259 | 15px / w400 / 行高20px / text/secondary |
| JS | 15px / w600（设计可变字重590） / 行高20px / text/brand |
| John Smith | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Bank of America ···· 7781 | 15px / w400 / 行高20px / text/secondary |
| LW | 15px / w600（设计可变字重590） / 行高20px / text/brand |
| Lim Wei | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| DBS Bank ···· 4521 | 15px / w400 / 行高20px / text/secondary |

#### EZB · 选了联系人 · 回到本页回填（只读）（1935:2538）

已取得详细上下文；完整视觉与交互仍待校准。

| 已读显示文本（动态样例不作为默认值） | 文字属性原始读取 |
| --- | --- |
| Their bank details | 28px / w700 / 行高33px / text/primary |
| We send in US dollars by SWIFT. | 15px / w400 / 行高20px / text/secondary |
| Country | 13px / w400 / 行高18px / text/disabled |
| United Arab Emirates | 17px / w500（设计可变字重510） / 行高23px / text/disabled |
| IBAN | 13px / w400 / 行高18px / text/disabled |
| AE07 0331 2345 6789 0123 456 | 17px / w500（设计可变字重510） / 行高23px / text/disabled |
| 23 characters, starts with AE | 13px / w400 / 行高18px / text/tertiary |
| SWIFT / BIC code | 13px / w400 / 行高18px / text/disabled |
| EBILAEAD | 17px / w500（设计可变字重510） / 行高23px / text/disabled |
| Emirates NBD · Dubai | 13px / w400 / 行高18px / text/tertiary |
| In your payees | 13px / w400 / 行高18px / text/secondary |
| AM | 15px / w600（设计可变字重590） / 行高20px / text/brand |
| AL MANSOORI TRADING LLC | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Emirates NBD ···· 3456 | 15px / w400 / 行高20px / text/secondary |
| Continue | 17px / w600（设计可变字重590） / 行高23px / text/on-brand |

#### EZB · 无 IBAN 的国家（填账号）（1754:3956）

已取得详细上下文；完整视觉与交互仍待校准。

| 已读显示文本（动态样例不作为默认值） | 文字属性原始读取 |
| --- | --- |
| Their bank details | 28px / w700 / 行高33px / text/primary |
| We send in US dollars by SWIFT. | 15px / w400 / 行高20px / text/secondary |
| Country | 13px / w400 / 行高18px / text/tertiary |
| Singapore | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Account number | 13px / w400 / 行高18px / text/tertiary |
| 0123 4567 89 | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| As shown on their bank statement | 13px / w400 / 行高18px / text/tertiary |
| SWIFT / BIC code | 13px / w400 / 行高18px / text/tertiary |
| DBSSSGSG | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| DBS Bank · Singapore | 13px / w400 / 行高18px / text/tertiary |
| Check these with your recipient | 17px / w600（设计可变字重590） / 行高23px / text/primary |
| Money sent to a wrong account may be hard to get back. | 15px / w400 / 行高20px / text/secondary |
| Continue | 17px / w600（设计可变字重590） / 行高23px / text/on-brand |

#### EZB · 美国（账号 + ABA）（1756:4028）

已取得详细上下文；完整视觉与交互仍待校准。

| 已读显示文本（动态样例不作为默认值） | 文字属性原始读取 |
| --- | --- |
| Their bank details | 28px / w700 / 行高33px / text/primary |
| We send in US dollars by SWIFT. | 15px / w400 / 行高20px / text/secondary |
| Country | 13px / w400 / 行高18px / text/tertiary |
| United States | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Account number | 13px / w400 / 行高18px / text/tertiary |
| 4831 0076 2259 | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| As shown on their bank statement | 13px / w400 / 行高18px / text/tertiary |
| ABA routing number | 13px / w400 / 行高18px / text/tertiary |
| 026 009 593 | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| 9 digits · on their cheque or bank app | 13px / w400 / 行高18px / text/tertiary |
| SWIFT / BIC code | 13px / w400 / 行高18px / text/tertiary |
| BOFAUS3N | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Bank of America · New York | 13px / w400 / 行高18px / text/tertiary |
| Check these with your recipient | 17px / w600（设计可变字重590） / 行高23px / text/primary |
| Money sent to a wrong account may be hard to get back. | 15px / w400 / 行高20px / text/secondary |
| Continue | 17px / w600（设计可变字重590） / 行高23px / text/on-brand |

#### EZB · SWIFT 查不到（1754:4008）

已取得详细上下文；完整视觉与交互仍待校准。

| 已读显示文本（动态样例不作为默认值） | 文字属性原始读取 |
| --- | --- |
| Their bank details | 28px / w700 / 行高33px / text/primary |
| We send in US dollars by SWIFT. | 15px / w400 / 行高20px / text/secondary |
| Country | 13px / w400 / 行高18px / text/tertiary |
| United Arab Emirates | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| IBAN | 13px / w400 / 行高18px / text/tertiary |
| AE07 0331 2345 6789 0123 456 | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| 23 characters, starts with AE | 13px / w400 / 行高18px / text/tertiary |
| SWIFT / BIC code | 13px / w400 / 行高18px / 颜色待校准 |
| EBILAEXX | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| We can't find a bank with this code. | 13px / w400 / 行高18px / 颜色待校准 |
| Check these with your recipient | 17px / w600（设计可变字重590） / 行高23px / text/primary |
| Money sent to a wrong account may be hard to get back. | 15px / w400 / 行高20px / text/secondary |
| Continue | 17px / w600（设计可变字重590） / 行高23px / text/disabled |

#### EZB · IBAN 格式不对（1754:4059）

已取得详细上下文；完整视觉与交互仍待校准。

| 已读显示文本（动态样例不作为默认值） | 文字属性原始读取 |
| --- | --- |
| Their bank details | 28px / w700 / 行高33px / text/primary |
| We send in US dollars by SWIFT. | 15px / w400 / 行高20px / text/secondary |
| Country | 13px / w400 / 行高18px / text/tertiary |
| United Arab Emirates | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| IBAN | 13px / w400 / 行高18px / 颜色待校准 |
| AE07 0331 2345 6789 | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| This IBAN doesn't look right. Check the country code and the digits. | 13px / w400 / 行高18px / 颜色待校准 |
| SWIFT / BIC code | 13px / w400 / 行高18px / text/tertiary |
| EBILAEAD | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Emirates NBD · Dubai | 13px / w400 / 行高18px / text/tertiary |
| Check these with your recipient | 17px / w600（设计可变字重590） / 行高23px / text/primary |
| Money sent to a wrong account may be hard to get back. | 15px / w400 / 行高20px / text/secondary |
| Continue | 17px / w600（设计可变字重590） / 行高23px / text/disabled |

#### EZB · 不支持的国家（1754:4110）

已取得详细上下文；完整视觉与交互仍待校准。

| 已读显示文本（动态样例不作为默认值） | 文字属性原始读取 |
| --- | --- |
| Their bank details | 28px / w700 / 行高33px / text/primary |
| We send in US dollars by SWIFT. | 15px / w400 / 行高20px / text/secondary |
| Country | 13px / w400 / 行高18px / 颜色待校准 |
| Iran | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| We can't send money to this country. | 13px / w400 / 行高18px / 颜色待校准 |
| Continue | 17px / w600（设计可变字重590） / 行高23px / text/disabled |

#### EZB · 选国家（1754:4168）

仅结构已读；详细文案、布局、颜色、图标与状态尚待补读。


**本页仍需校准的业务边界：**

- 支持国家、IBAN／ABA／加拿大分支、城市和州字典及地址必填配置；改变国家后清除规则；T4是否同步最新城市Other规则？（待校准）

## §2 T3-02 收款人和地址

1. **页面与标题：**返回银行页；Who gets the money? 与说明使用本流程标题规格。姓名、Their address 分组、国家、城市及条件地址字段依次排列；组标题20px，字重／行高及分组上下间距（待校准）。姓名字段不拆企业／个人。
2. **字段：**姓名、City／City name、街道、邮编、美国州／ZIP 均用标准字段；选择项右箭头，手输项无箭头。Country 与既有联系人资料只读但保留正常字色。国家字段配置、街道／州的准确标签和可选标记（待校准）。
3. **城市半框：**搜索、滚动城市列表、底部固定 Other；无结果显示 Use “{输入}” 和 Enter it as your city。选中 Other 后展开 City name；展开间距、无结果字号／行高与边距（待校准）。没有字典时直接文本输入，不伪造候选列表。
4. **动作与退出：**首个可编辑必填输入自动聚焦，长表单避让键盘。原图注为 Continue 跟随内容，当前 UI 采用固定安全底栏以保证可达；最终底栏布局（待校准）。Continue 只进入金额，不保存联系人或单独认证；返回保持本轮普通输入，生产草稿（待校准）。

**逐元素与状态细则：**

- 标题Who gets the money?，说明Use the name on their bank account.；Name on their account只一个字段，不区分个人／企业。新建时仅示例占位，不预填企业示例。
- Their address：Country沿用上页只读、City必填；基线Street and building (optional)与Post code (optional)。美国街道、州与ZIP必填，单元选填；其他国家附加要求必须来自确认后的配置。
- 配城市列表的国家：City为可搜索下拉，Other固定半框底部不随列表滚动；搜索模糊匹配，大小写／空格／连字符不敏感。无结果提供Use “{输入}”／Enter it as your city，点击后City=Other、City name预填该输入。选择Other展开City name；完全未配置城市列表时直接文本框、无下拉箭头。
- 当前合成规则清除依赖国家的银行／地址与旧报价，保留无关输入；真实字段依赖（待校准）。缺城市阻断并报错，完整验证规则不从其他国家复制。
- 长表单可滚动；原图注 Continue 跟内容之后，当前 UI 采用固定安全底栏，最终布局（待校准）。银行资料不可改的既有联系人仍可回前页重选，不能把只读做成禁用灰字。
- Continue进入金额；此时不保存联系人、不要求单独保存PIN。


### T3-02 收款人信息 · 状态文案与属性（待校准）


#### EZB · 默认（空）（1959:4630）

已取得详细上下文；完整视觉与交互仍待校准。

| 已读显示文本（动态样例不作为默认值） | 文字属性原始读取 |
| --- | --- |
| Who gets the money? | 28px / w700 / 行高33px / text/primary |
| Use the name on their bank account. | 15px / w400 / 行高20px / text/secondary |
| Name on their account | 13px / w400 / 行高18px / text/tertiary |
| Full name or company name | 17px / w500（设计可变字重510） / 行高23px / text/disabled |
| Their address | 20px / w600（设计可变字重590） / 行高27px / text/primary |
| Country | 13px / w400 / 行高18px / 颜色待校准 |
| United Arab Emirates | 17px / w500（设计可变字重510） / 行高23px / 颜色待校准 |
| City | 13px / w400 / 行高18px / text/primary |
| e.g. Dubai | 17px / w500（设计可变字重510） / 行高23px / text/disabled |
| Street and building (optional) | 13px / w400 / 行高18px / text/tertiary |
| e.g. Office 1204, Al Moosa Tower | 17px / w500（设计可变字重510） / 行高23px / text/disabled |
| Post code (optional) | 13px / w400 / 行高18px / text/tertiary |
| e.g. 00000 | 17px / w500（设计可变字重510） / 行高23px / text/disabled |
| Continue | 17px / w600（设计可变字重590） / 行高23px / text/disabled |

#### EZB · 默认（1754:4202）

已取得详细上下文；完整视觉与交互仍待校准。

| 已读显示文本（动态样例不作为默认值） | 文字属性原始读取 |
| --- | --- |
| Who gets the money? | 28px / w700 / 行高33px / text/primary |
| Use the name on their bank account. | 15px / w400 / 行高20px / text/secondary |
| Name on their account | 13px / w400 / 行高18px / text/tertiary |
| AL MANSOORI TRADING LLC | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Their address | 20px / w600（设计可变字重590） / 行高27px / text/primary |
| Country | 13px / w400 / 行高18px / 颜色待校准 |
| United Arab Emirates | 17px / w500（设计可变字重510） / 行高23px / 颜色待校准 |
| City | 13px / w400 / 行高18px / text/tertiary |
| Dubai | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Street and building (optional) | 13px / w400 / 行高18px / text/tertiary |
| Office 1204, Al Moosa Tower | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Post code (optional) | 13px / w400 / 行高18px / text/tertiary |
| Continue | 17px / w600（设计可变字重590） / 行高23px / text/on-brand |

#### EZB · 选城市（预设列表 + Other 兜底）（2583:2649）

已取得详细上下文；完整视觉与交互仍待校准。

| 已读显示文本（动态样例不作为默认值） | 文字属性原始读取 |
| --- | --- |
| Who gets the money? | 28px / w700 / 行高33px / text/primary |
| Use the name on their bank account. | 15px / w400 / 行高20px / text/secondary |
| Name on their account | 13px / w400 / 行高18px / text/tertiary |
| AL MANSOORI TRADING LLC | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Their address | 20px / w600（设计可变字重590） / 行高27px / text/primary |
| Country | 13px / w400 / 行高18px / 颜色待校准 |
| United Arab Emirates | 17px / w500（设计可变字重510） / 行高23px / 颜色待校准 |
| City | 13px / w400 / 行高18px / text/tertiary |
| Dubai | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Street and building (optional) | 13px / w400 / 行高18px / text/tertiary |
| Office 1204, Al Moosa Tower | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Post code (optional) | 13px / w400 / 行高18px / text/tertiary |
| Continue | 17px / w600（设计可变字重590） / 行高23px / text/on-brand |
| Search city | 17px / w400 / 行高23px / text/tertiary |
| Abu Dhabi | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Sharjah | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Ajman | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Fujairah | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Ras Al Khaimah | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Umm Al Quwain | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Other | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Not listed? Type the city name | 15px / w400 / 行高20px / text/tertiary |

#### EZB · 搜不到城市 → 用输入的字（3118:2915）

已取得详细上下文；完整视觉与交互仍待校准。

| 已读显示文本（动态样例不作为默认值） | 文字属性原始读取 |
| --- | --- |
| Who gets the money? | 28px / w700 / 行高33px / text/primary |
| Use the name on their bank account. | 15px / w400 / 行高20px / text/secondary |
| Name on their account | 13px / w400 / 行高18px / text/tertiary |
| AL MANSOORI TRADING LLC | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Their address | 20px / w600（设计可变字重590） / 行高27px / text/primary |
| Country | 13px / w400 / 行高18px / 颜色待校准 |
| United Arab Emirates | 17px / w500（设计可变字重510） / 行高23px / 颜色待校准 |
| City | 13px / w400 / 行高18px / text/tertiary |
| Dubai | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Street and building (optional) | 13px / w400 / 行高18px / text/tertiary |
| Office 1204, Al Moosa Tower | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Post code (optional) | 13px / w400 / 行高18px / text/tertiary |
| Continue | 17px / w600（设计可变字重590） / 行高23px / text/on-brand |
| Al Dhaid | 17px / w400 / 行高23px / text/primary |
| No city found | 17px / w400 / 行高23px / text/tertiary |
| Use “Al Dhaid” | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Enter it as your city | 15px / w400 / 行高20px / text/tertiary |
| Other | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Not listed? Type the city name | 15px / w400 / 行高20px / text/tertiary |

#### EZB · 城市选了 Other · 自己填（2583:2769）

仅结构已读；详细文案、布局、颜色、图标与状态尚待补读。

#### EZB · 国家没配城市列表 → 文本框（2874:2538）

仅结构已读；详细文案、布局、颜色、图标与状态尚待补读。

#### EZB · 选了联系人 · 姓名与地址只读（1939:22765）

仅结构已读；详细文案、布局、颜色、图标与状态尚待补读。

#### EZB · 美国地址（州 + ZIP）（1756:4089）

仅结构已读；详细文案、布局、颜色、图标与状态尚待补读。

#### EZB · 缺城市（1754:4302）

已取得详细上下文；完整视觉与交互仍待校准。

| 已读显示文本（动态样例不作为默认值） | 文字属性原始读取 |
| --- | --- |
| Who gets the money? | 28px / w700 / 行高33px / text/primary |
| Use the name on their bank account. | 15px / w400 / 行高20px / text/secondary |
| Name on their account | 13px / w400 / 行高18px / text/tertiary |
| AL MANSOORI TRADING LLC | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Their address | 20px / w600（设计可变字重590） / 行高27px / text/primary |
| Country | 13px / w400 / 行高18px / 颜色待校准 |
| United Arab Emirates | 17px / w500（设计可变字重510） / 行高23px / 颜色待校准 |
| City | 13px / w400 / 行高18px / 颜色待校准 |
| Enter the city. | 13px / w400 / 行高18px / 颜色待校准 |
| Street and building (optional) | 13px / w400 / 行高18px / text/tertiary |
| Office 1204, Al Moosa Tower | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Post code (optional) | 13px / w400 / 行高18px / text/tertiary |
| Continue | 17px / w600（设计可变字重590） / 行高23px / text/disabled |

## §3 T3-03 金额、费用与用途

1. **页面与布局：**返回地址页；标题及收款人副文、金额、Available／International limit left、费用卡、用途、Continue。金额及焦点沿用行内规格，费用卡外边距、内边距和分组间距（待校准）。
2. **费用卡：**Who pays fees 为可选行；Fee 为只读行。标签和值分别使用 `textSecondary`／`textPrimary`，具体字号、行高、分隔线（待校准）。优惠原价划线，新价或 Free 与说明 label／info 同行，空间不足自然换行；划线颜色、标签表面与命中区（待校准）。
3. **用途：**必选下拉，空占位、已选值与就近 Choose a purpose. 错误态；条目精确排序和最终字典（待校准）。当前 UI 金额有效且非试算中时可点 Continue 校验用途；金额无效或报价加载中阻断。用途仅属本笔交易。
4. **数据一致：**当前 OUR 用合成固定总价，SHA／BEN／优惠为独立快照；正式计价（待校准）。金额或费用变化使旧报价失效；试算失败提示、重试与按钮恢复（待校准），不能显示旧价却提交新价。

**逐元素与状态细则：**

标题How much to send?，副文To {姓名} · {银行}；金额、余额、额度和系统小数键盘参照T2金额规格，明确国际限额为International limit left。金额不是余额展示组件，不套用52→30缩放。

| 项目 | 行为与文案 |
| --- | --- |
| Who pays fees | 默认Shared (SHA)，可点击进入T3-04 |
| Fee | 只读费用；不进入未采用的Fee details页面 |
| SHA | 图示$15.00，仅展示占位，不作为定价规则 |
| OUR | 图示固定总价，旧注释存在后补扣与不补扣冲突，（待校准） |
| BEN | Paid by them，不估算对方收到金额 |
| 优惠 | Fee后带可点label与信息图标；原价划线＋Free／新价，覆盖减价、免费次数、首笔免费；活动说明半框。条件、活动结束时间和文案由确认配置决定，不能用设计示例当正式活动 |
| Purpose of transfer | 每笔必选，不保存到联系人。空值点Continue显示Choose a purpose.；清单尚为占位，不视为最终业务选项 |

设计占位用途依次Payment for goods／Payment for services／Family support／Salary or wages／Investment／Other。独立T3-05用途页不做。当前金额有效且非试算中允许 Continue 校验用途，金额无效／试算中阻断；生产完整状态矩阵（待校准）。


### T3-03 金额与费用 · 状态文案与属性（待校准）


#### EZB · 默认 SHA（822:3818）

已取得详细上下文；完整视觉与交互仍待校准。

| 已读显示文本（动态样例不作为默认值） | 文字属性原始读取 |
| --- | --- |
| How much to send? | 28px / w700 / 行高33px / text/primary |
| To AL MANSOORI TRADING LLC · Emirates NBD | 15px / w400 / 行高20px / text/secondary |
| 8,500 | 字号待校准 / 待校准 / 行高待校准 / text/primary |
| Who pays fees | 15px / w400 / 行高20px / text/secondary |
| Shared (SHA) | 15px / w600（设计可变字重590） / 行高20px / text/primary |
| Fee | 15px / w400 / 行高20px / text/secondary |
| $15.00 | 15px / w600（设计可变字重590） / 行高20px / text/primary |
| Available $128,450.20 · International limit left $45,000.00 | 13px / w400 / 行高18px / text/secondary |
| Purpose of transfer | 13px / w400 / 行高18px / text/tertiary |
| Payment for services | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Continue | 17px / w600（设计可变字重590） / 行高23px / text/on-brand |

#### EZB · 选汇款用途（底部弹层）（2878:3107）

已取得详细上下文；完整视觉与交互仍待校准。

| 已读显示文本（动态样例不作为默认值） | 文字属性原始读取 |
| --- | --- |
| How much to send? | 28px / w700 / 行高33px / text/primary |
| To AL MANSOORI TRADING LLC · Emirates NBD | 15px / w400 / 行高20px / text/secondary |
| 8,500 | 字号待校准 / 待校准 / 行高待校准 / text/primary |
| Who pays fees | 15px / w400 / 行高20px / text/secondary |
| Shared (SHA) | 15px / w600（设计可变字重590） / 行高20px / text/primary |
| Fee | 15px / w400 / 行高20px / text/secondary |
| $15.00 | 15px / w600（设计可变字重590） / 行高20px / text/primary |
| Available $128,450.20 · International limit left $45,000.00 | 13px / w400 / 行高18px / text/secondary |
| Purpose of transfer | 13px / w400 / 行高18px / text/tertiary |
| Payment for services | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Continue | 17px / w600（设计可变字重590） / 行高23px / text/on-brand |
| Payment for goods | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Family support | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Salary or wages | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Investment | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Other | 17px / w500（设计可变字重510） / 行高23px / text/primary |

#### EZB · 没选用途点 Continue（2878:3316）

仅结构已读；详细文案、布局、颜色、图标与状态尚待补读。

#### EZB · 手续费优惠（定稿 · 行内 label）· 金额页（2019:2713）

仅结构已读；详细文案、布局、颜色、图标与状态尚待补读。

#### EZB · 手续费优惠（定稿） B 减价 · 金额页（2048:11124）

仅结构已读；详细文案、布局、颜色、图标与状态尚待补读。

#### EZB · 手续费优惠（定稿） C 免费次数 · 金额页（2048:11174）

仅结构已读；详细文案、布局、颜色、图标与状态尚待补读。

#### EZB · 手续费优惠（定稿） D 首笔免费 · 金额页（2048:11224）

仅结构已读；详细文案、布局、颜色、图标与状态尚待补读。

#### EZB · 手续费优惠（定稿）· 点 label 弹说明（2108:11167）

仅结构已读；详细文案、布局、颜色、图标与状态尚待补读。

#### EZB · 选了 OUR（822:3905）

仅结构已读；详细文案、布局、颜色、图标与状态尚待补读。

#### EZB · 选了 BEN（1314:2588）

仅结构已读；详细文案、布局、颜色、图标与状态尚待补读。

#### EZB · 超国际限额（复用 CA3-05）（822:3928）

仅结构已读；详细文案、布局、颜色、图标与状态尚待补读。


**本页仍需校准的业务边界：**

- OUR采用固定总价不再补扣，还是旧说明“他行费后补扣”？SHA／OUR示例$15／$45都不能直接变正式定价。BEN扣费展示口径也需确认。（待校准）
- Purpose占位清单的正式选项与空值验证；用途是每笔必选但未选时Continue是否可点触发错误？（待校准）

## §4 T3-04 谁付费用半框

1. **结构：**标题 Who pays the fees?，SHA／OUR／BEN 三个单选项，SHA 带推荐标识。选项标题、副说明、费用值及选中标记的精确字号、间距、背景与图标（待校准）；不引入未采用的优惠 banner。
2. **选择与取消：**选中立即收起并刷新费用；外点／下滑／系统返回取消时维持原选项，最终关闭行为（待校准）。刷新失败如何恢复选项和报价（待校准）。当前 OUR 固定总价仅为 Mock，BEN 不预估收款金额。

**逐元素与状态细则：**

标题Who pays the fees?；依次SHA（推荐）、OUR、BEN，单选，选后自动收起并刷新费用。BEN只解释费用从对方收款扣；OUR按最终确认规则写固定价。长说明、选中标记、推荐标签、每项精确文案和取消行为尚待补读（待校准），不额外塞入未采用的优惠banner。


### T3-04 谁付费用 · 状态文案与属性（待校准）


#### EZB · 费用选项（822:4070）

仅结构已读；详细文案、布局、颜色、图标与状态尚待补读。

## §5 T3-06 复核与Reference

1. **页面与顺序：**返回金额页，标题 Check and send；防诈提示、收付款信息、Reference／Purpose、费用与合计、截止／锁价说明、认证按钮。下文列出的字段顺序为已读依据；最终分组、间距和编辑入口（待校准）。
2. **Reference 半框：**pencil 为独立命中区至少44px，资源名／尺寸／颜色（待校准）。标准选填输入，当前按35个用户可见字符计数，不另加字符白名单；保存更新，Cancel／返回不改原值。标题、占位、计数位置、空值展示与允许字符的正式规则（待校准）。
3. **金额与优惠：**You send／Our fee／You pay 取同份确认快照；金额当前用正式34px，其他字段按本流程正文语义。原价、优惠价、节省金额的字段文案与完整样式（待校准）。BEN 不推算对方实收。
4. **锁价与过期：**展示当前报价及倒计时；到期禁止旧价提交，重取后弹新价确认，同意后重新认证；取消、编辑 Reference 均不能绕过新价同意。倒计时字号、警示色、过期半框完整文案与操作（待校准）；有效期、前后台重新取价及失败策略（待校准）。
5. **确认与退出：**认证复用 T2，操作对应当前报价快照；处理中防重复。返回保留本轮普通输入，不保存认证结果；截止日、时区、节假日与发出日期（待校准），不自行承诺到账日。

**逐元素与状态细则：**

标题Check and send；顶部提醒Do you know and trust this business?／EZB will never ask you to move money to keep it safe.，为可配置防诈／公告位。按顺序To、From、Reference、Purpose、Who pays fees、You send、Our fee、You pay；有优惠同金额页显示，不重复计算出另一份金额。

Reference右侧pencil，点击半框编辑，选填最多35字符，可展示在收款人银行流水；当前按35个用户可见字符计数，取消不改原值；空值展示及生产允许字符（待校准）。其余字段是否可点回编辑（待校准）。

不承诺到账日；过截止时间只写哪天发出。截止时区、节假日和日期来源（待校准）。用户已确认定稿可见UI与交互纳入：换汇锁价、有效倒计时、过期重确认按设计状态展示并使用Mock；有效期与重新确认交互仍逐项校准，不接真实汇率服务。Confirm with Face ID及指纹、PIN、FV异常复用T2认证能力，不能跳过当前操作的安全上下文。


### T3-06 复核 · 状态文案与属性（待校准）


#### EZB · 常规（822:4313）

已取得详细上下文；完整视觉与交互仍待校准。

| 已读显示文本（动态样例不作为默认值） | 文字属性原始读取 |
| --- | --- |
| Check and send | 28px / w700 / 行高33px / text/primary |
| Do you know and trust this business? | 17px / w600（设计可变字重590） / 行高23px / text/primary |
| EZB will never ask you to move money to keep it safe. | 15px / w400 / 行高20px / text/secondary |
| To | 13px / w400 / 行高18px / text/tertiary |
| AL MANSOORI TRADING LLC · Emirates NBD · AE07 ···· 3456 | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| From | 13px / w400 / 行高18px / text/tertiary |
| USD Current account · ···· 4821 | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Reference | 13px / w400 / 行高18px / text/tertiary |
| INV-2026-0918 | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Purpose | 13px / w400 / 行高18px / text/tertiary |
| Payment for services | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| Who pays fees | 13px / w400 / 行高18px / text/tertiary |
| Shared (SHA) | 17px / w500（设计可变字重510） / 行高23px / text/primary |
| You send | 15px / w400 / 行高20px / text/secondary |
| $8,500.00 | 15px / w600（设计可变字重590） / 行高20px / text/primary |
| Our fee | 15px / w400 / 行高20px / text/secondary |
| $15.00 | 15px / w600（设计可变字重590） / 行高20px / text/primary |
| You pay | 15px / w400 / 行高20px / text/secondary |
| $8,515.00 | 17px / w600（设计可变字重590） / 行高23px / text/primary |
| Other banks may deduct a fee from what they receive. We'll show it once the money arrives. | 13px / w400 / 行高18px / text/secondary |
| Confirm with Face ID | 17px / w600（设计可变字重590） / 行高23px / text/on-brand |

#### EZB · 手续费优惠（定稿 · 行内 label）· 复核页（2019:2794）

仅结构已读；详细文案、布局、颜色、图标与状态尚待补读。

#### EZB · 点 Reference 编辑（1968:10555）

仅结构已读；详细文案、布局、颜色、图标与状态尚待补读。

#### EZB · 选了 OUR（1963:24272）

仅结构已读；详细文案、布局、颜色、图标与状态尚待补读。

#### EZB · 选了 BEN（1314:2674）

仅结构已读；详细文案、布局、颜色、图标与状态尚待补读。

#### EZB · 过了截止时间（822:4392）

仅结构已读；详细文案、布局、颜色、图标与状态尚待补读。

#### 一期 · 换汇锁定汇率（822:4468）

仅结构已读；详细文案、布局、颜色、图标与状态尚待补读。

#### 一期 · 汇率过期（822:4564）

仅结构已读；详细文案、布局、颜色、图标与状态尚待补读。


**本页仍需校准的业务边界：**

- 截止时间时区、节假日、发出日期、锁价过期及前后台重新取价；优惠资格、次数、结束时间及说明内容？（待校准）

## §6 T3-07／08 结果、进度和退回

1. **已提交结果页：**状态图形、标题、说明、Done、View details；采用 T2 结果页排版，SWIFT 的准确标题、图形、说明与间距（待校准）。默认仅表示已提交；Done 回 Payment，详情显示同笔交易，不生成另一笔。
2. **进度详情：**显示本笔金额、对象、银行与账号、费用和进度；完整字段、步骤文案、时间戳、已完成／当前／未完成节点样式（待校准）。他行费未确认时不伪造实收，最终补充时点（待校准）。
3. **退回与异常：**处理中、复核、失败、未知、退回分别展示；退回原因、退款状态、Help／查询动作及返回（待校准）。未知只查同笔交易，不重复付款。对账完成后再写回余额，不承诺即时退款。
4. **联系人与通知：**当前默认已提交不自动保存新联系人；真实成功保存与列表排序（待校准）。到账后通知仅作说明，最终渠道与文案（待校准），不接旧短信服务。

**逐元素与状态细则：**

- 默认已提交，不称到账成功；Done回T1，View details进T3-08。人工复核、失败、网络未知复用T2对应状态的结构与返回规则，具体SWIFT差异（待校准）。
- 不写具体到账日期，只说明到账后通知。UI期只模拟通知相关状态，不接真实通知服务。
- 详情复用活期结构，覆盖处理中和退回；实际他行费用到账后补充展示，不提前伪造。退款须对账完成后回余额，不承诺即时。
- 设计旧注释提到退回短信＋推送，与本轮不接真实服务及短信删除背景不同，通知渠道须明确；不从旧代码自动接短信。
- 自动存联系人以“转出成功”说明为候选，已提交／Processing即更新T1展示的规则与此存在边界问题，集中（待校准）。

### T3-07 已提交 · 状态文案与属性（待校准）


#### EZB · 已提交（822:4620）

仅结构已读；详细文案、布局、颜色、图标与状态尚待补读。


### T3-08 进度与退回 · 状态文案与属性（待校准）


#### EZB · 处理中（复用活期详情）（822:4706）

仅结构已读；详细文案、布局、颜色、图标与状态尚待补读。

#### EZB · 被退回（复用活期详情）（822:4771）

仅结构已读；详细文案、布局、颜色、图标与状态尚待补读。


**本页仍需校准的业务边界：**

- 结果、退回通知最终渠道；真实消息服务另期，本期只Mock；不依据旧短信注释接入服务。（待校准）
