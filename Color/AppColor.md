# AppColor · EZB 颜色与主题契约

> **来源口径：**按当前颜色、主题和组件代码整理。现有色值保持不变；本文记录字段、明暗值及 KYC 使用语义，不创建新的颜色类。
>
> **校准口径：**颜色值为代码现值；页面如何使用、亮色最终呈现与供应商主题能力仍需校准。本文与 KYC 页面只在本契约库内部互引。

## §1 颜色体系与主题机制

1. 应用同时存在旧静态 `AppColor` 与新语义 `EzbSemanticColors`。它们不是同一组颜色；不能因文件名为 AppColor 就把新 KYC 全部改为旧蓝色。
2. 旧 `AppColor` 的九个字段是静态常量，不随主题切换。其全表见 §3，供历史页面识别，不用于新增 KYC 取色。
3. 新 KYC 通过当前主题的 `context.ezbColors` 取得语义色；下表中的字段名就是实际语义字段，不另建同名静态转发表。
4. 根应用在浅色与深色主题上分别挂载对应的语义扩展，保留历史组件样式。挂载语义扩展不等于旧页面自动改用新颜色。
5. 当前启动逻辑优先检查“跟随系统”，否则按“深色”开关选明暗；两个历史开关默认均为 false，所以现状首次默认浅色。KYC 目标为跟随用户设置，不擅自重置全局偏好；是否迁移为默认跟随系统（待校准）。
6. 当前设置切换会触发全局强制刷新，系统栏也存在固定配置；不能据此声称已经满足无状态丢失和系统栏同步。目标：保留表单及页面栈，状态栏/导航栏/键盘随模式（待校准）。
7. 暗色和亮色均使用 §2 的实际值；不从暗色自动反色，也不把旧 `primaryText` 等静态值假定为暗色白字。
8. 透明色写作 `#RRGGBB × 不透明度`，不是在现值上再乘透明度。已有 alpha 不重复叠加；Flutter 的八位写法为 alpha 前缀，不与色值尾缀混淆。

## §2 新 KYC 语义色全表

以下 58 个字段已逐项对照当前运行时颜色与两套主题输入，暗色在前、亮色在后。

### §2.1 品牌

| 语义名称 | 实际字段 | 暗色 | 亮色 |
| --- | --- | --- | --- |
| `brand/ink` | `brandInk` | #0C1B26 | #0C1B26 |
| `brand/primary` | `brandPrimary` | #0FA5F0 | #0FA5F0 |
| `brand/primary-hover` | `brandPrimaryHover` | #17B4F7 | #0E93D6 |
| `brand/primary-press` | `brandPrimaryPress` | #0E8BD0 | #0B7CB8 |
| `brand/silver` | `brandSilver` | #E8EEF2 | #E8EEF2 |

### §2.2 背景与表面

| 语义名称 | 实际字段 | 暗色 | 亮色 |
| --- | --- | --- | --- |
| `bg/base` | `bgBase` | #0A1620 | #EFF3F7 |
| `bg/brand-selected` | `bgBrandSelected` | #0FA5F0 × 24% | #CDE6F8 |
| `bg/brand-subtle` | `bgBrandSubtle` | #0FA5F0 × 12% | #E4F1FB |
| `bg/control-ghost` | `bgControlGhost` | #FFFFFF × 8% | #E9EFF4 |
| `bg/control-off` | `bgControlOff` | #FFFFFF × 12% | #D5DFE7 |
| `bg/disabled` | `bgDisabled` | #FFFFFF × 8% | #E3EAF1 |
| `bg/elevated` | `bgElevated` | #101F2B | #FFFFFF |
| `bg/error-tint` | `bgErrorTint` | #F2555A × 12% | #FBE8E9 |
| `bg/field` | `bgField` | #FFFFFF × 5% | #F5F8FA |
| `bg/glass` | `bgGlass` | #FFFFFF × 6% | #FFFFFF × 78% |
| `bg/inverse` | `bgInverse` | #E8EEF2 | #0C1B26 |
| `bg/nav-glass` | `bgNavGlass` | #0C1B26 × 58% | #FFFFFF × 80% |
| `bg/on-color-subtle` | `bgOnColorSubtle` | #FFFFFF × 22% | #FFFFFF × 22% |
| `bg/overlay-scrim` | `bgOverlayScrim` | #0A1620 × 72% | #0C1B26 × 40% |
| `bg/surface-1` | `bgSurface1` | #0C1B26 | #FFFFFF |
| `bg/surface-2` | `bgSurface2` | #13232F | #E8EEF4 |
| `bg/surface-hover` | `bgSurfaceHover` | #FFFFFF × 9% | #E4EBF1 |
| `bg/surface-raised` | `bgSurfaceRaised` | #FFFFFF × 5% | #FFFFFF |
| `bg/track` | `bgTrack` | #FFFFFF × 16% | #D8E2EA |

### §2.3 文字

| 语义名称 | 实际字段 | 暗色 | 亮色 |
| --- | --- | --- | --- |
| `text/brand` | `textBrand` | #0FA5F0 | #0A6FAD |
| `text/disabled` | `textDisabled` | #FFFFFF × 30% | #8A9AA7 |
| `text/on-brand` | `textOnBrand` | #06202E | #06202E |
| `text/on-color` | `textOnColor` | #FFFFFF | #FFFFFF |
| `text/on-color-secondary` | `textOnColorSecondary` | #FFFFFF × 62% | #FFFFFF × 70% |
| `text/primary` | `textPrimary` | #FFFFFF | #0C1B26 |
| `text/secondary` | `textSecondary` | #93A8B6 | #4A5F6E |
| `text/static-dark` | `textStaticDark` | #0C1B26 | #0C1B26 |
| `text/static-light` | `textStaticLight` | #FFFFFF | #FFFFFF |
| `text/tertiary` | `textTertiary` | #7C93A6 | #58697A |

### §2.4 图标

| 语义名称 | 实际字段 | 暗色 | 亮色 |
| --- | --- | --- | --- |
| `icon/brand` | `iconBrand` | #0FA5F0 | #0A6FAD |
| `icon/on-brand` | `iconOnBrand` | #06202E | #06202E |
| `icon/on-color` | `iconOnColor` | #FFFFFF | #FFFFFF |
| `icon/on-color-muted` | `iconOnColorMuted` | #FFFFFF × 60% | #FFFFFF × 70% |
| `icon/primary` | `iconPrimary` | #FFFFFF | #0C1B26 |
| `icon/secondary` | `iconSecondary` | #93A8B6 | #4A5F6E |
| `icon/tertiary` | `iconTertiary` | #7C93A6 | #58697A |

### §2.5 描边

| 语义名称 | 实际字段 | 暗色 | 亮色 |
| --- | --- | --- | --- |
| `border/control` | `borderControl` | #FFFFFF × 40% | #778C9C |
| `border/focus` | `borderFocus` | #0FA5F0 | #0A6FAD |
| `border/glass-edge` | `borderGlassEdge` | #FFFFFF × 26% | #FFFFFF × 70% |
| `border/row` | `borderRow` | #FFFFFF × 8% | #E6ECF1 |
| `border/strong` | `borderStrong` | #FFFFFF × 22% | #778C9C |
| `border/subtle` | `borderSubtle` | #FFFFFF × 10% | #DDE5EC |

### §2.6 反馈

| 语义名称 | 实际字段 | 暗色 | 亮色 |
| --- | --- | --- | --- |
| `feedback/error` | `feedbackError` | #F2555A | #C0272E |
| `feedback/error-bg` | `feedbackErrorBg` | #F2555A × 14% | #FBE8E9 |
| `feedback/info` | `feedbackInfo` | #0FA5F0 | #0A6FAD |
| `feedback/success` | `feedbackSuccess` | #56B99C | #1B7A5C |
| `feedback/success-bg` | `feedbackSuccessBg` | #17C29A × 14% | #E3F4EA |
| `feedback/warning` | `feedbackWarning` | #F5A524 | #A34A06 |
| `feedback/warning-bg` | `feedbackWarningBg` | #F5A524 × 14% | #FDF1E1 |

### §2.7 应用内键盘

| 语义名称 | 实际字段 | 暗色 | 亮色 |
| --- | --- | --- | --- |
| `system/kb-bg` | `systemKbBg` | #1C1C1E | #D1D4DA |
| `system/kb-key` | `systemKbKey` | #6A6A6E | #FFFFFF |
| `system/kb-key-alt` | `systemKbKeyAlt` | #4A4A4E | #ADB3BD |
| `system/kb-label` | `systemKbLabel` | #FFFFFF | #000000 |

## §3 旧 AppColor 静态值

全部为明暗同值，不把这些值用于新版 KYC 的页面背景、文字或 CTA。

| 字段 | 当前值 | 历史语义 |
| --- | --- | --- |
| `scaffoldBackground` | #FFFFFF | 旧页面背景 |
| `primaryBackground` | #0D2E73 | 旧主背景/顶栏 |
| `primaryText` | #333333 | 旧主要文字 |
| `secondaryText` | #666666 | 旧次要文字 |
| `accentColor` | #0D2E57 | 旧强调色 |
| `secondaryColor` | #FECD67 | 旧次要品牌色 |
| `warnColor` | #FAA634 | 旧警告 |
| `borderColor` | #DEDEDE | 旧边框 |
| `dividerColor` | #F2F2F2 | 旧分隔线 |

## §4 历史主题容器现状

| 区域 | 浅色现状 | 暗色现状 | 新 KYC 调用口径 |
| --- | --- | --- | --- |
| 旧页面壳底色 | #F5F7FD | #000000 × 54% | 使用 `bgBase`，避免沿用旧壳底色 |
| 旧顶栏 | `primaryBackground` | 同值 | 内容页使用 `bgBase`，返回按钮复用 `EzbAppBar` |
| 旧主要文字 | `primaryText` | 同值 | 改用对应 `textPrimary` 等语义字段 |
| 旧底部导航底色 | #FFFFFF | #000000 × 54% | KYC 不因历史导航值推定新底部布局 |
| 旧导航选中色 | `accentColor` | 同值 | 新页面 CTA/选项分别用其明确语义 |
| 旧导航未选中色 | #A2A5B9 | 同值 | 新页面不以此代替 `iconSecondary` |

## §5 KYC 按场景取色

| 场景 | 背景 | 文字 / 图标 | 状态补充 |
| --- | --- | --- | --- |
| 页面、普通顶部区 | `bgBase` | `textPrimary` / `iconPrimary` | 说明 `textSecondary`，辅助 `textTertiary` |
| 字段 | `bgField` | 值 `textPrimary`，标签 `textSecondary` | 焦点 `borderFocus`；错误底 `bgErrorTint`，文字 `feedbackError` |
| 单选行未选 | `bgSurface2` | `textPrimary`、`textSecondary`、`iconSecondary` | 圈底 `bgControlOff` |
| 单选行选中 | `bgBrandSelected`（待校准） | `textPrimary`，勾底 `iconBrand` | 页面画面与组件说明的选中底不一致（待校准） |
| Chip 未选 | `bgSurfaceRaised` | `textPrimary` | 无描边 |
| Chip 选中 | `brandPrimary`（待校准） | `textOnBrand` | 页面使用实色，组件说明使用浅品牌底（待校准） |
| 主按钮 | `brandPrimary` | `textOnBrand` | 按下色是否切 `brandPrimaryPress`（待校准），现有按钮关闭独立按下覆盖 |
| 次按钮 | `bgSurface2` | `textPrimary` | 文字型次操作使用 `textBrand` |
| 禁用按钮 | `bgDisabled` | `textDisabled` | 不可点击 |
| 内容弹层 | `bgElevated` | `textPrimary` / `textSecondary` | 抓手 `bgTrack`，遮罩 `bgOverlayScrim` |
| 信息/提醒卡 | `bgGlass` | `textPrimary` / `textSecondary` | 玻璃降级使用 `bgSurface2`，不新增色 |
| 错误、警告、成功 | 对应 `feedback*Bg` | 对应 `feedbackError` / `feedbackWarning` / `feedbackSuccess` | 是反馈语义，不随涨跌偏好变化 |
| PIN 键盘 | `systemKbBg` / `systemKbKey` / `systemKbKeyAlt` | `systemKbLabel` | 圆点另按 PIN 页规定 |
| 实时相机上的固定浅色控件 | 相机画面 | `textStaticLight` / `iconOnColor` | 普通内容区不使用静态白冒充主题文字 |

## §6 局部固定颜色与限制

1. 现有顶栏图标玻璃层含局部色 #0C1B26 × 34%，阴影 #000000 × 18%；弹层阴影为 #000000 × 32%。这些是现有组件内部值，不是新语义字段，KYC 不复制成私有常量。
2. 结果页渐变与发光的两套主题色没有完整对应字段。先按已有 `brandPrimary` 与 `bgBase` 混合过渡、光晕使用 `brandPrimary` 的 12%（待校准）；这是视觉候选，不能据此改写颜色表或新增 token。
3. 补件清单中的分隔线是否保留、字段常规边框是否保留、选项与 Chip 选中底色均按页面标注逐项校准，不根据旧组件自动决定。

文字对比度至少4.5:1、大字至少3:1，图标与控件至少3:1；相机和渐变背景分别核对。
