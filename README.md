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
