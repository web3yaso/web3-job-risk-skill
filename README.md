# Web3 Job Risk · 求职尽职调查 Skill

> A Claude skill for Web3 job seekers to assess offer risk before signing.
> 帮助 Web3 求职者在入职前识别 Offer 风险的 Claude Skill。

Built by [@web3law_tech](https://x.com/web3law_tech)

---

## What It Does · 功能介绍

This skill turns Claude into a **Web3 offer risk analyst** — combining industry expertise with real-time web research to evaluate job opportunities across 5 dimensions.

本 Skill 将 Claude 转变为一名 **Web3 Offer 风险分析师**，结合行业专业知识与实时网络调研，从 5 个维度评估求职机会。

**Two-phase output · 两阶段输出：**
1. 🔍 **Risk Scorecard** — 5-dimension red/yellow/green assessment（风险评估卡，即时输出）
2. 📋 **Full Report** — detailed evidence, red flags, and pre-offer questions to ask（完整报告，按需生成）

---

## 5 Assessment Dimensions · 5 大评估维度

| Dimension · 维度 | Core Question · 核心问题 |
|---|---|
| 🏛️ Regulatory Compliance · 监管合规 | Will this role expose me to personal legal liability? 这个岗位会让我承担个人法律责任吗？ |
| 💰 Salary Safety · 薪资安全性 | Will the company still exist in 6 months? 公司 6 个月后还在吗？ |
| 🪙 Token Risk · Token 风险 | Is the token portion of my offer actually worth anything? Offer 中的 Token 部分能拿到吗？ |
| 👥 Team Credibility · 团队可信度 | Does this team have the ability and intent to deliver? 这个团队有能力且有意愿兑现承诺吗？ |
| 🔍 Project Authenticity · 项目真实性 | Is this project real, or just a show for investors? 这个项目是真实运营的吗？ |

---

## What Makes This Different · 差异化定位

Most job evaluation tools focus on salary and culture. This skill focuses on what most Web3 guides miss: **your employer's legal exposure becomes your legal exposure the moment you sign.**

大多数求职评估工具关注薪资和文化。本 Skill 关注的是大多数 Web3 求职指南忽略的核心问题：**入职的那一刻，雇主的监管风险就会传导给你。**

Built on real legal case knowledge from Chinese Web3 criminal defense practice, including:
基于中国 Web3 刑事辩护实务案例知识库，涵盖：

- 帮信罪 / 非法经营罪 / 开设赌场罪 employee liability cases（员工刑事责任案例）
- 4 categories of high-risk platform patterns with real case numbers（四类高危平台模式，含真实案号）
- Jurisdiction-specific regulatory signals: SEC, SFC, MAS, OSC, FINTRAC（多司法管辖区监管信号）
- Agency employer dual-layer risk assessment（Agency 类雇主双层风险评估）
- Fraud detection layer: fake Zoom attacks, ClickFix, Lazarus/BlueNoroff threat intelligence（诈骗前置过滤层）

---

## How to Use · 使用方法

### Option 1: Use with Claude directly · 直接在 Claude 中使用

1. Open a new conversation with Claude
2. Paste the contents of `SKILL.md` as your first message, or ask Claude to read it from this repo
3. Then type: `帮我评估 [公司名] 的 offer 风险` or `Assess the risk of a job offer at [company name]`

### Option 2: API integration · API 集成

Use `SKILL.md` as the system prompt in your Anthropic API call. Enable the `web_search` tool for real-time research.

将 `SKILL.md` 作为 system prompt 传入 Anthropic API，并开启 `web_search` 工具以支持实时调研。

```javascript
const response = await fetch("https://api.anthropic.com/v1/messages", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    "x-api-key": process.env.ANTHROPIC_API_KEY,
    "anthropic-version": "2023-06-01"
  },
  body: JSON.stringify({
    model: "claude-sonnet-4-20250514",
    max_tokens: 4000,
    system: SKILL_MD_CONTENT, // contents of SKILL.md
    tools: [{ type: "web_search_20250305", name: "web_search" }],
    messages: [{ role: "user", content: userInput }]
  })
});
```

---

## File Structure · 文件结构

```
web3-job-risk/
├── SKILL.md                    # Main skill file · 主文件（流程 + 输出模板）
├── README.md                   # This file · 本文件
└── references/
    ├── risk-criteria.md        # Risk judgment criteria · 风险判断标准（评估时按需读取）
    ├── scam-patterns.md        # Scam pattern library · 诈骗手法识别库（诈骗过滤时读取）
    └── legal-cases.md          # Legal cases & practice · 法律案例与实务（评估法律风险时读取）
```

---

## Sample Output · 输出示例

```
🔍 Stratosphere / Movimentum · Social Media Manager Offer 风险评估

| 维度               | 状态 | 核心发现                                  |
|--------------------|------|-------------------------------------------|
| 🏛️ 监管合规风险   | 🟡   | SMM岗在部分司法管辖区存在内容推介责任风险  |
| 💰 薪资安全性      | 🟡   | 小型私人机构，无公开融资记录              |
| 🪙 Token风险       | 🟢   | 法币薪资结构，未提及token薪酬             |
| 👥 团队可信度      | 🟡   | 客户名单可核实，但创始人背景公开度低      |
| 🔍 项目真实性      | 🟢   | 有可核实客户案例，业务模式清晰            |

综合判断：🟡 可以推进，但有 2 个问题需要入职前确认

需要查看完整分析报告吗？
```

---

## Disclaimer · 免责声明

This skill generates preliminary risk screening reports based on publicly available information. It does not constitute legal advice. For specific legal questions, please consult a licensed attorney.

本 Skill 基于公开信息生成初步风险筛查报告，不构成法律建议。具体法律问题请咨询执业律师。

---

## About · 关于

**[@web3law_tech](https://x.com/web3law_tech)** focuses on the intersection of Web3, legal compliance, and content. This skill is part of the [web3law.tech](https://web3law.tech) platform — tools for Web3 professionals navigating legal and regulatory complexity.

**[@web3law_tech](https://x.com/web3law_tech)** 专注于 Web3、法律合规与内容的交汇地带。本 Skill 是 [web3law.tech](https://web3law.tech) 平台的一部分——为 Web3 从业者提供法律合规导航工具。

---

*Contributions and feedback welcome. If you've encountered a Web3 job risk scenario not covered here, open an issue.*
*欢迎贡献和反馈。如果你遇到了本 Skill 未覆盖的 Web3 求职风险场景，欢迎提 issue。*
