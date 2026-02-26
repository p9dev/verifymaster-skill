# VerifyMaster（查证大师）— 技能仓库

> 本文件供公开技能仓库使用：在新仓库中可将本文件作为 **README.zh-CN.md**，将同目录下的 **README.verifymaster-skill.md** 作为 **README.md**。

本仓库提供 **VerifyMaster（查证大师）** 的 AI Agent 技能定义文件 `skill.md`，便于在 [OpenClaw](https://github.com/OpenClaw) 或其它支持技能发现的 Agent 中使用查证服务。

---

## 什么是查证大师？

**查证大师（VerifyMaster）** 是一个智能内容验证平台，帮助用户甄别网络信息的**真实性**和**逻辑合理性**。

### 核心能力

- **事实核查**：验证文章、新闻、社交媒体中的核心论据是否属实，与权威数据源交叉验证。
- **逻辑分析**：识别常见逻辑谬误与诡辩手法（如稻草人谬误、滑坡谬论、诉诸权威、以偏概全等）。
- **多类型输入**：支持**文本**、**URL 链接**、**图片**、**PDF**、**音频**、**视频**，一次提交即可获得综合报告。
- **多语言**：界面与结果支持中文、英文等，便于全球化使用。

### 适用场景举例

| 场景 | 说明 |
|------|------|
| 健康与养生 | 验证「某食物防癌」「某疗法包治」等说法，减少健康谣言误导。 |
| 新闻与热点 | 核查突发新闻、网传截图、聊天记录中的事实与来源。 |
| 社交媒体 | 快速判断朋友圈、群聊、短视频中的信息是否可信。 |
| 学习与写作 | 检查论据是否可靠、论证是否存在逻辑漏洞，辅助批判性思维。 |
| AI Agent / 自动化 | 通过 API 或本仓库的 skill 将查证能力接入对话助手、工作流等。 |

### 结果报告包含什么？

- **事实核查清单**：逐条标注核心论据的验证状态（已验证为真 / 部分真实 / 虚假 / 无法验证）。
- **逻辑分析**：指出文中的逻辑谬误类型与位置，并给出简要说明。
- **综合评估**：事实可信度与逻辑严密度评分，以及总体判定（可信 / 部分可信 / 误导性 / 虚假）。
- **参考文献**：权威资料来源与链接，便于进一步查阅。

---

## 链接与资源

| 资源 | 链接 |
|------|------|
| **官方网站** | [https://verifymaster.info](https://verifymaster.info) |
| **API 文档** | [https://verifymaster.info/docs](https://verifymaster.info/docs) |
| **For AI / Agent 说明** | [https://verifymaster.info/docs/for-ai](https://verifymaster.info/docs/for-ai) |
| **OpenAPI 规范** | [https://api.verifymaster.info/v1/openapi.json](https://api.verifymaster.info/v1/openapi.json) |
| **AI Plugin 清单** | [https://api.verifymaster.info/.well-known/ai-plugin.json](https://api.verifymaster.info/.well-known/ai-plugin.json) |
| **Skill 文件（本技能）** | [https://api.verifymaster.info/.well-known/skill.md](https://api.verifymaster.info/.well-known/skill.md) |

---

## 本仓库内容

- **`skill.md`**：OpenClaw 等 Agent 可用的技能定义，含 YAML frontmatter 与 OpenAI Function Calling 风格的工具定义（登录、查配额、提交查证、轮询状态、获取结果等）。
- **`README.zh-CN.md`**：本说明（中文）。
- **`README.md`**：英文说明。

### 如何使用本技能

1. **方式一：添加本仓库为技能源**  
   在 OpenClaw 或支持「从 Git 仓库加载技能」的 Agent 中，添加本仓库地址作为技能源，即可使用 `skill.md` 中定义的工具调用 VerifyMaster API。

2. **方式二：使用 Skill 的直链**  
   若工具支持「通过 URL 添加技能」，可使用上述 **Skill 文件** 链接：  
   `https://api.verifymaster.info/.well-known/skill.md`

3. **API 与认证**  
   - 需先调用 `POST /v1/auth/login` 获取 JWT，再在请求头中携带 `Authorization: Bearer <token>` 调用其它接口。  
   - 完整接口说明见 [API 文档](https://verifymaster.info/docs) 与 [For AI 说明](https://verifymaster.info/docs/for-ai)。

---

## 注册与使用

- 在 [verifymaster.info](https://verifymaster.info) 注册账号后，即可在网页端使用查证功能，或通过 API / 本技能在 Agent 中使用。
- 免费版提供每日一定次数的文本查证；订阅或积分可解锁更多次数与类型（图片、PDF、音视频等）。具体计费见官网与 API 文档。

---

## 许可与联系

- 本仓库中的 `skill.md` 与 README 仅供说明与集成使用。
- 查证服务的使用受 [VerifyMaster 服务条款](https://verifymaster.info) 与相关政策约束。
- 问题或建议可联系：support@verifymaster.info。
