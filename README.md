# Foreign Law Research Skill / 域外法查明技能

**[English](#english) | [中文](#中文)**

---

## English

A structured skill for AI coding assistants to **research and ascertain foreign law** — featuring a court-aligned ascertainment methodology (modeled on the Shanghai Financial Court's *Guidelines on the Ascertainment of Foreign Law*, 2025), a curated index of **121 free legal databases**, and an **open-source legal data layer** (git-versioned law corpora, open-data collection scripts, MCP servers).

Output is submission-grade: an **Ascertainment Opinion** (six-part judicial format) plus a **Research Log** (search audit trail), with mandatory AI-tool disclosure — ready for cross-examination in PRC cross-border proceedings. Bilingual: the Chinese edition ships in this same repository — [跳转到中文版](#中文).

### What's new in v2.0

| Area | v1.0 | v2.0 |
|------|------|------|
| Methodology | Six-step research flow | Scoping (Step 0) + six steps, aligned with judicial ascertainment standards (Arts. 4, 5, 7, 10, 12, 14, 19–22, 24 of the Guidelines) |
| Deliverables | Cited research results | Six-part **Ascertainment Opinion** + **Research Log**, with AI-tool disclosure and expert-signature blocks |
| Quality assurance | Risk checklist | Point-in-time validity verification + five-point cross-examination self-check |
| Data sources | 121 web databases | + open-source layer: [lexifina/global-law](https://github.com/lexifina/global-law) (law on any date, CC0), [worldwidelaw/legal-sources](https://github.com/worldwidelaw/legal-sources) (110+ countries), [Ansvar Systems](https://github.com/Ansvar-Systems) MCP gateway (28 jurisdictions) |
| Languages | Chinese only | **Bilingual**: `域外法查明/` (Chinese) and `foreign-law-research/` (English), each a complete native skill |

### Repository structure

```
├── README.md                        # This file (bilingual)
├── CHANGELOG.md
├── 域外法查明/                        # Chinese skill
│   ├── SKILL.md                     # v2.0 methodology (Chinese triggers + English triggers)
│   └── references/
│       ├── 数据库索引.md              # 121 databases by jurisdiction
│       ├── 开源数据源.md              # open-source data layer guide
│       ├── 查明意见书模板.md          # Ascertainment Opinion template
│       └── 查明工作记录模板.md        # Research Log template
└── foreign-law-research/             # English skill (mirror structure)
    ├── SKILL.md
    └── references/
        ├── database-index.md
        ├── open-source-data.md
        ├── opinion-template.md
        └── research-log-template.md
```

### Installation & usage

#### Claude Code (native support)

```bash
cd your-project
mkdir -p .claude/skills && cd .claude/skills
git clone https://github.com/StefanCHEN2026/foreign-law-research-skill-.git
```

Then just ask in Chinese or English. The skill auto-triggers on phrases like:

- ZH: "域外法"、"外国法"、"海外法律"、"比较法"、"外国法律查明"、"域外法律研究"、"涉外法律"、"查明某国法律"
- EN: "foreign law ascertainment", "ascertain the law of [country]", "overseas/foreign law research", "comparative law research", "what does [country] law say about…"

#### Other AI tools

| Tool | How |
|------|-----|
| **Cursor** | Copy `SKILL.md` into `.cursor/rules/` as an `.mdc` rule file |
| **Codex / OpenAI** | Paste `SKILL.md` as a system prompt or upload as a knowledge file |
| **GitHub Copilot** | Extract the workflow into `.github/copilot-instructions.md` |
| **Others** | Use the methodology as custom instructions / system prompt |

The methodology and the references are platform-agnostic.

#### Optional: connect the open-source data layer

```bash
# Ansvar gateway — 28 jurisdictions' national law + EU law + domain corpora (OAuth, free tier)
claude mcp add ansvar --transport http https://gateway.ansvar.eu/mcp

# lexifina/global-law — local MCP over git-versioned law (Python 3.9+ + git, no network)
git clone --depth 1 https://github.com/lexifina/global-law
# see foreign-law-research/references/open-source-data.md for setup
```

### Workflow overview

| Step | Content |
|------|---------|
| 0 | Scoping — disputes, governing law, facts, question list, channels, deadline (Art. 4) |
| 1 | Jurisdiction identification (+ federal/multi-level systems; HK/Macau/Taiwan & treaties in scope, Art. 24) |
| 2 | Sources of law and their hierarchy |
| 3 | Identifying specific legal instruments |
| 4 | Locating specific rules (+ citation resolution, point-in-time lookup) |
| 5 | Quality assurance — validity verification + five-point cross-examination self-check (Art. 14) |
| 6 | Deliverables — Ascertainment Opinion (six parts, Art. 10) + Research Log (Art. 12) + AI disclosure |

Plus: the nine ascertainment channels map (Art. 5), non-ascertainment criteria and PRC-law fallback (Arts. 20–21), and an optional PRC comparative-law perspective.

### Data coverage

- **121 free databases** across 30+ jurisdictions, three authority tiers (🟢 official / 🟡 LII·academic / 🔵 third-party): US, UK, EU, Canada, Australia, Singapore, Hong Kong, Japan, South Korea, France, Germany, Switzerland, plus UN, WTO, WIPO, ICJ and other international bodies
- **Open-source layer** (🟣/⚙️/🔌): law on any date with per-word provenance (lexifina), official bulk/API endpoints for 110+ countries and a 16M-document search API (worldwidelaw/legal-sources + legaldatahunter.com), and MCP servers for 28 European jurisdictions + EU law with verbatim citations (Ansvar)

### License

MIT — see [LICENSE](LICENSE). The referenced open-source projects keep their own licenses (lexifina CC0; Ansvar Apache-2.0; per-country corpora terms).

### Contributing

Issues and PRs welcome: database additions/corrections, new-jurisdiction guides, methodology improvements, platform adaptations.

---

## 中文

适用于 AI 编程助手的**域外法律查明技能**：查明方法论对标《上海金融法院外国法查明工作指引》（2025），内置 **121 个全球免费法律数据库**索引与**开源法律数据层**（git 版本化法律库、开放数据采集清单、MCP 服务器）。

产出为**司法提交级**双交付物：《外国法律查明意见书》（六部分结构）+《外国法律查明工作记录》（检索留痕），并强制附 AI 工具披露——可直接用于涉外民商事案件的外国法查明与质证。

### v2.0 升级亮点

| 方面 | v1.0 | v2.0 |
|------|------|------|
| 方法论 | 六步法检索流程 | 步骤 0「查明范围界定」+ 六步法，全流程对标司法查明标准（指引第 4、5、7、10、12、14、19–22、24 条） |
| 交付物 | 带引用的研究结果 | 六部分《外国法律查明意见书》+《外国法律查明工作记录》，内置 AI 披露与专家签署栏 |
| 质量审查 | 风险清单 | 任意日期点查法核验效力 + 质证自检五项 |
| 数据来源 | 121 个网站数据库 | + 开源数据层：[lexifina/global-law](https://github.com/lexifina/global-law)（任意日期查法，CC0）、[worldwidelaw/legal-sources](https://github.com/worldwidelaw/legal-sources)（110+ 国）、[Ansvar Systems](https://github.com/Ansvar-Systems) MCP 网关（28 法域） |
| 语言 | 仅中文 | **中英双版**：`域外法查明/`（中文）与 `foreign-law-research/`（英文），各自为完整可用的原生 skill |

### 仓库结构

```
├── README.md                        # 本文件（双语）
├── CHANGELOG.md
├── 域外法查明/                        # 中文版技能
│   ├── SKILL.md                     # v2.0 方法论（中文触发词 + 英文触发词）
│   └── references/
│       ├── 数据库索引.md              # 121 个数据库，按法域归类
│       ├── 开源数据源.md              # 开源数据层使用指南
│       ├── 查明意见书模板.md          # 查明意见书模板
│       └── 查明工作记录模板.md        # 查明工作记录模板
└── foreign-law-research/             # 英文版技能（结构对称）
    ├── SKILL.md
    └── references/
        ├── database-index.md
        ├── open-source-data.md
        ├── opinion-template.md
        └── research-log-template.md
```

### 安装与使用

#### Claude Code（原生支持）

```bash
cd 你的项目目录
mkdir -p .claude/skills && cd .claude/skills
git clone https://github.com/StefanCHEN2026/foreign-law-research-skill-.git
```

安装后在对话中出现以下关键词即可自动触发：
- "域外法"、"外国法"、"海外法律"、"比较法"、"外国法律查明"、"域外法律研究"、"涉外法律"、"查明某国法律"
- 英文提问同样触发："ascertain the law of…"、"what does [country] law say about…" 等

#### 其他 AI 工具

| 工具 | 使用方式 |
|------|----------|
| **Cursor** | 将 `SKILL.md` 转为 `.cursor/rules/` 下的 `.mdc` 规则文件 |
| **Codex / OpenAI** | 将 `SKILL.md` 内容作为 system prompt 或上传为 knowledge file |
| **GitHub Copilot** | 提取流程写入 `.github/copilot-instructions.md` |
| **其他工具** | 方法论与 references 均平台无关，可作 custom instructions 使用 |

#### 可选：接入开源数据层

```bash
# Ansvar 网关 — 28 法域国家法 + EU 法 + 专题库（OAuth，有免费档）
claude mcp add ansvar --transport http https://gateway.ansvar.eu/mcp

# lexifina/global-law — 本地 MCP，git 版本化法律库（Python 3.9+ 与 git，零网络请求）
git clone --depth 1 https://github.com/lexifina/global-law
# 配置方法见 域外法查明/references/开源数据源.md
```

### 流程概览

| 步骤 | 内容 |
|------|------|
| 0 | 查明范围界定 — 争议、准据法、事实、问题清单、途径、时限（第 4 条） |
| 1 | 识别法域（联邦/多层级体系；港澳台与条约参照适用，第 24 条） |
| 2 | 识别法律渊源及位阶 |
| 3 | 识别具体法律法规 |
| 4 | 定位具体规则（引证解析、任意日期点查） |
| 5 | 质量审查 — 效力核验 + 质证自检五项（第 14 条） |
| 6 | 输出 — 查明意见书（六部分，第 10 条）+ 工作记录（第 12 条）+ AI 披露 |

另含：九大查明途径全景（第 5 条）、不能查明的认定与中国法兜底（第 20–21 条）、可选的中国比较法视角。

### 数据覆盖

- **121 个免费数据库**，覆盖 30+ 法域，三级权威标记（🟢 官方 / 🟡 LII·学术 / 🔵 第三方）：美国、英国、欧盟、加拿大、澳大利亚、新加坡、香港、日本、韩国、法国、德国、瑞士等，以及联合国、WTO、WIPO、国际法院等国际组织
- **开源数据层**（🟣/⚙️/🔌）：任意日期点查法条并逐字溯源（lexifina）、110+ 国官方批量/API 端点目录与 1600 万文档检索 API（worldwidelaw/legal-sources + legaldatahunter.com）、28 个欧洲法域 + EU 法的 MCP 检索且结果带逐字引证（Ansvar）

### 许可证

MIT — 详见 [LICENSE](LICENSE)。所引用的开源项目保留各自许可（lexifina CC0；Ansvar Apache-2.0；各国语料库遵循其条款）。

### 贡献

欢迎提交 Issue 和 PR：数据库条目增补/修正、新法域操作指南、方法论改进、平台适配。
