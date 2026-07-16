# AI Social Media Ops Skills

让 OpenClaw / Cursor 把社媒运营从「每天想选题」变成一条可复盘的 AI 工作流。

这是一套基于标准 `SKILL.md` 格式的开源社媒运营技能集，覆盖：

**热点与竞品监控 → 选题与脚本框架 → 多平台改写 → 人工发布 → 数据复盘 → 爆款规律回流**

默认只读取公开信息，所有发布动作由人工确认，适合个人创作者、小团队和多账号运营者。

## 为什么值得用

- **每天知道发什么**：监控行业热点与竞品内容，生成带理由、钩子和脚本框架的选题日报。
- **一稿适配多平台**：针对抖音、视频号、公众号、YouTube、X、Instagram、TikTok 和 Amazon Shop 分别改写。
- **不是只看播放量**：按账号自身基线识别爆款与哑弹，沉淀真正可复用的内容规律。
- **越用越懂账号**：复盘结论会回流到下一轮选题，而不是每次从零开始。
- **人在回路**：不自动登录、不自动发帖，降低误发、违规和封号风险。
- **配置与内容分离**：个人账号、竞品和业务信息只写在本地 `config.yaml`，不会进入公开仓库。

## 三个技能模块

| 模块 | 解决的问题 | 触发示例 |
| --- | --- | --- |
| [`trend-topic-radar`](trend-topic-radar/) | 监控热点与竞品，产出选题日报、开头钩子和脚本框架 | `用选题雷达跑一遍今天的选题` |
| [`content-publish`](content-publish/) | 将一条内容改写成不同平台的发布素材包 | `把选题库第 1 条改写成抖音和公众号版本` |
| [`analytics`](analytics/) | 汇总表现数据，识别爆款规律并给出下一周期建议 | `用这周的数据做一次复盘` |

## 工作流

```text
选题雷达
   ↓
成稿 / 可选接入视频工厂
   ↓
多平台内容适配
   ↓
人工审核并发布
   ↓
数据复盘
   ↓
规律回流，下一轮选题更准确
```

## 安装

### OpenClaw：从 GitHub 安装

```bash
git clone https://github.com/yt203677-debug/ai-social-media-ops.git
cd ai-social-media-ops
openclaw skills install ./trend-topic-radar
openclaw skills install ./content-publish
openclaw skills install ./analytics
```

也可以将三个模块目录平级复制到 workspace 的 `skills/` 目录：

```text
<workspace>/skills/
├── trend-topic-radar/
├── content-publish/
└── analytics/
```

### Cursor / 其他兼容 Agent

将三个模块目录复制到项目的 `.cursor/skills/` 或目标 Agent 的 skills 目录。

> 三个模块需要保持平级：`content-publish` 和 `analytics` 会读取 `../trend-topic-radar/config.yaml`。

## 首次配置

每个模块都提供可安全公开的 `config.example.yaml`。首次使用前：

1. 把需要使用的模块中的 `config.example.yaml` 复制为 `config.yaml`。
2. 填写产品定位、目标人群、关键词、竞品、目标平台和复盘规则。
3. 直接用自然语言触发对应技能。

```bash
# 示例（Windows PowerShell）
Copy-Item trend-topic-radar/config.example.yaml trend-topic-radar/config.yaml
Copy-Item content-publish/config.example.yaml content-publish/config.yaml
Copy-Item analytics/config.example.yaml analytics/config.yaml
```

`config.yaml`、选题库、发布库和复盘数据均已被 `.gitignore` 排除，不会意外提交。

## 输出示例

### 选题日报

每条选题包含：

- 为什么现在做、目标人群痛点
- 相关性评分、内容角度
- 开头 3 秒钩子、脚本框架
- 平台适配建议、来源与风险提示

### 多平台发布素材包

同一内容会分别生成各平台适用的标题、正文、标签、封面建议、发布时间和人工发布清单。

### 数据复盘报告

按账号自身中位数识别爆款/平款/哑弹，输出 Top/Bottom 内容、爆款共性、失败假设和下一周期行动建议。

## 安全与隐私

- 只读取公开数据；可选的后台读取模式也必须保持只读。
- 不自动登录、发布、点赞、私信或修改账号设置。
- 所有内容默认是草稿，必须人工审核。
- 不编造无法取得的数据，缺失项明确标记为“无数据”。
- 本地 `config.yaml` 和运行产物不会被 Git 跟踪。

## 目录结构

```text
ai-social-media-ops/
├── README.md
├── LICENSE
├── trend-topic-radar/
│   ├── SKILL.md
│   ├── config.example.yaml
│   ├── reference.md
│   └── templates/
├── content-publish/
│   ├── SKILL.md
│   ├── config.example.yaml
│   ├── reference.md
│   └── templates/
└── analytics/
    ├── SKILL.md
    ├── config.example.yaml
    ├── reference.md
    └── templates/
```

## 适合谁

- 同时运营多个社媒平台的个人创作者
- 需要标准化选题、分发和复盘流程的小团队
- 希望用 OpenClaw / Cursor 构建内容运营工作流的开发者
- 想先保证安全可控，再逐步增加自动化能力的运营者

## License

[MIT](LICENSE)
