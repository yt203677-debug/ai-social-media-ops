# 指标定义 · 数据获取 · 爆款判定 · 闭环说明

## 一、核心指标与跨平台归一
不同平台叫法不同，复盘时统一成下列字段（能拿到多少填多少）：

| 统一字段 | 抖音/视频号/TikTok | 公众号 | YouTube | X/Instagram |
| --- | --- | --- | --- | --- |
| 曝光 impressions | 推荐播放/曝光 | 送达/展示 | impressions | impressions |
| 观看/阅读 views | 播放量 | 阅读量 | views | 视频观看/展示 |
| 互动 likes/comments/shares | 赞/评/藏/转 | 赞/在看/分享 | like/comment | like/reply/repost |
| 完成度 completion | 完播率 | 阅读完成率 | 平均观看时长% | 视频完播率 |
| 涨粉 new_followers | 新增粉丝 | 新增关注 | subscribers | followers |
| 转化 conversion | 主页访问/私信/组件点击 | 文末点击/回复 | 点击/描述链接 | 链接点击/主页访问 |

> 转化信号最重要（决定生意），能拿到就一定记录。

## 二、数据获取方式
### 方式1 · 手动导出/录入（默认，零风险）
- 各平台创作者后台一般可导出数据或看数据面板。把数值填入 `数据/entries.csv`（见 templates/data-entry.csv）。
- 也可把后台**截图**交给 AI，读图后转成表格再入 CSV。

### 方式2 · 浏览器只读（进阶，可选）
- 用 OpenClaw 浏览器接管**已登录**的创作者后台，只打开数据页面读取数字。
- 严格只读：不发帖、不改设置、不点赞私信。遇登录态失效/验证码，报"需人工处理"，不猜测、不硬闯。
- 控制频率，避免高频刷新后台。

#### 各平台数据页入口（URL 特征，供导航参考）
> 平台后台 DOM/域名会变，以下为大致特征；先按域名进创作者中心，再找"数据/数据中心/分析(Analytics)"。
> 读数时优先用页面可见的数字标签，不要依赖固定 CSS 选择器。取不到就转手动录入。

| 平台 | 后台域名/入口 | 数据页特征关键词 |
| --- | --- | --- |
| 抖音 | creator.douyin.com（创作者服务中心） | "数据中心""作品数据""粉丝数据" |
| 视频号 | channels.weixin.qq.com（微信视频号助手） | "数据""动态数据""内容分析" |
| 公众号 | mp.weixin.qq.com（公众平台） | "统计""内容分析""用户分析" |
| 快手 | cp.kuaishou.com | "数据中心""作品分析" |
| 小红书 | creator.xiaohongshu.com（蒲公英/创作中心） | "数据中心""笔记数据" |
| bilibili | member.bilibili.com（创作中心） | "数据中心""视频数据""粉丝管理" |
| YouTube | studio.youtube.com | "Analytics""Content""Overview/Reach" |
| X (Twitter) | analytics.twitter.com 或 x.com 帖子 Analytics | "Impressions""Engagements" |
| Instagram | 需在 App/Meta Business Suite | "Insights""Reach""Interactions" |
| TikTok | tiktok.com/tiktokstudio 或 Creator Center | "Analytics""Video views""Followers" |

- 单条内容数据：多数平台在"作品/视频详情页"或"内容分析"里可看单条曝光/播放/互动。
- 抓到后按 [templates/data-entry.csv](templates/data-entry.csv) 的列结构落表，再进入判定。

### 方式3 · 官方数据 API
- 若某平台（如公众号、YouTube、X）有开放的数据统计 API，可后续接入自动拉取。

## 三、爆款判定（相对基线，避免绝对数字误导）
- 按平台、按指标，取该账号该指标的**中位数**作基线。
- 爆款：核心指标 ≥ `hit_multiplier` × 中位数（默认 3×）。
- 哑弹：< 0.5 × 中位数。
- 其余为平款。
- 样本太少（<5 条）时，判定仅供参考，报告里标注"样本不足"。
- 核心指标默认取 `观看/阅读`；若配置了转化 KPI，则优先看转化。

## 四、爆款规律沉淀
- 写入 `爆款规律库/patterns.md`，累积不覆盖。
- 每条规律记录：特征描述（选题方向/钩子/句式/形式/时长/时间/平台）+ 支撑案例（哪几条内容）+ 出现次数。
- 只把"重复出现 ≥2 次"的特征当规律，单次爆款记为"待验证"。

## 五、与选题雷达的闭环
- analytics 每次复盘后更新 `爆款规律库/patterns.md` 和报告里的「给选题雷达的建议」。
- 选题雷达（trend-topic-radar）在产出选题前，可读取本模块的 `爆款规律库/patterns.md`，
  优先复用已验证有效的选题方向与钩子、规避已被证明的哑弹方向。
- 建议把"给选题雷达的建议"里确认长期有效的方向，手动同步进 `trend-topic-radar/config.yaml` 的 keywords/方向。

```
选题雷达 ──产出──▶ 发布 ──数据──▶ analytics 复盘 ──规律回流──▶ 选题雷达(更准)
```
