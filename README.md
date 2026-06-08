# 域外法查明技能 / Foreign Law Research Skill

适用于 AI 编程助手的域外法律查明技能，内嵌标准化六步法查明流程和 121 个全球免费开放法律数据库索引。

> A structured skill for AI coding assistants to research foreign and overseas laws, featuring a six-step methodology and a curated index of 121+ free legal databases worldwide.

## 文件结构

```
skills/
├── README.md
├── LICENSE
└── 域外法查明/
    ├── SKILL.md                    # 主技能文件：六步法流程 + 使用说明
    └── references/
        └── 数据库索引.md            # 121个数据库索引，按法域归类
```

## 安装与使用

### Claude Code（原生支持）

**方法一：克隆到项目 skills 目录**
```bash
cd 你的项目目录
mkdir -p .claude/skills
cd .claude/skills
git clone https://github.com/StefanCHEN2026/foreign-law-research-skill-.git
```

**方法二：直接下载**
```bash
# 下载后解压到任意项目的 .claude/skills/ 目录下即可
```

安装后在 Claude Code 对话中包含以下关键词即可自动触发：
- "域外法"、"外国法"、"海外法律"、"比较法"
- "外国法律查明"、"域外法律研究"、"涉外法律"
- "查明某国法律"、提及具体国家/地区法律问题

### 其他 AI 工具

| 工具 | 使用方式 |
|------|----------|
| **Cursor** | 复制 `SKILL.md` 到 `.cursor/rules/域外法查明.mdc` |
| **Codex / OpenAI** | 将 `SKILL.md` 内容粘贴为 system prompt 或上传为 knowledge file |
| **GitHub Copilot** | 提取关键流程写入 `.github/copilot-instructions.md` |
| **其他工具** | 将六步法流程作为 custom instructions / system prompt 使用 |

核心方法论与平台无关，`references/数据库索引.md` 可独立作为参考文档查阅。

### 手动触发（任何平台）

如果工具不支持自动加载，直接在对话开头粘贴以下指令：

> 请按照域外法查明六步法流程：识别法域 → 识别法律渊源 → 识别具体法律法规 → 定位具体规则 → 质量审查 → 输出来源引用。

---

## 功能概览

| 步骤 | 内容 |
|------|------|
| 一 | 识别法域 (Jurisdiction Identification) |
| 二 | 识别该法域的法律渊源 (Sources of Law) |
| 三 | 识别具体的法律法规名称 (Identify Legal Instruments) |
| 四 | 定位具体规则 (Locate Specific Rules) |
| 五 | 质量审查 — 指出可能的错误点 (Quality Assurance) |
| 六 | 输出信息来源 (Source Citation) |

**可选步骤**：中国比较法视角 — 中外法律比较分析。

## 数据库覆盖范围

覆盖 **30+ 法域** 的 121 个免费法律数据库，分为三个权威性等级：

- 🟢 官方来源（政府网站/国际组织）
- 🟡 LII/学术机构
- 🔵 第三方平台

包括：美国、英国、欧盟、加拿大、澳大利亚、新加坡、香港、日本、韩国、法国、德国、瑞士等主要法域，以及联合国、WTO、WIPO、国际法院等国际组织。

## 平台兼容性

此技能原始格式为 **Claude Code Skill**，核心内容（方法论+数据库索引）与工具无关，可适配以下平台：

| 平台 | 适配方式 |
|------|----------|
| **Claude Code** | 原生支持，使用 `SKILL.md` 格式 |
| **Cursor** | 将 `SKILL.md` 内容转为 `.cursor/rules/` 目录下的 `.mdc` 规则文件 |
| **Codex (OpenAI)** | 将流程作为 system prompt 或 knowledge base 导入 |
| **GitHub Copilot** | 提取关键内容加入 `.github/copilot-instructions.md` |
| **WindSurf / Cline / Continue** | 作为 `.rules` 或自定义指令文件导入 |
| **通用** | 核心方法论可直接作为 system prompt 使用 |

### 快速适配

将 `SKILL.md` 和 `references/数据库索引.md` 复制到对应平台的规则/指令目录即可。六步法流程和数据库索引是独立于平台的方法论内容，无需修改。

如需适配特定平台的格式，可提交 Issue 或 PR 讨论。

## 许可证

MIT License — 详见 [LICENSE](LICENSE)

## 贡献

欢迎提交 Issue 和 PR，包括但不限于：

- 新增/修正数据库条目
- 适配更多 AI 平台
- 改进查明方法论
- 补充特定法域的操作指南
