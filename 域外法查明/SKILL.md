---
name: 域外法查明
description: This skill should be used when the user asks to research foreign or overseas laws, mentions "域外法", "外国法", "海外法律", "比较法", "外国法律查明", "域外法律研究", "涉外法律", "查明某国法律", or asks about specific legal provisions in any jurisdiction outside mainland China, including but not limited to the United States, United Kingdom, European Union, Japan, South Korea, Singapore, Hong Kong, Australia, Canada, Germany, France, and other overseas jurisdictions.
version: 1.0.0
---

# 域外法查明技能

本技能用于指导律师和法律工作者系统性查明域外法律（中国大陆以外法域的法律法规、判例和国际条约）。遵循六步法流程，结合全球 120+ 免费开放法律数据库，输出可追溯、可验证的法律查明结果。

## 概述

域外法查明需要遵循严格的法学方法流程：从确定目标法域开始，逐层深入至具体法律规则，最终输出附带完整来源引用的查明结果。本技能提供标准化操作流程，同时内置 121 个海外免费法律数据库的索引，覆盖全球主要法域。

## 数据库资源

详细的数据库索引存储在 `references/数据库索引.md`，按法域归类组织，包含每个数据库的链接、主要内容、运营主体和语言信息。

**在开始查明前，先查阅 `references/数据库索引.md` 确定目标法域对应的可用数据库。** 数据库分为三个权威性等级：
- 🟢 官方来源 — 政府网站、国际组织官方网站，优先使用
- 🟡 LII/学术机构 — 数据质量高但可能有更新延迟
- 🔵 第三方平台 — 覆盖面广，须与官方来源交叉验证

---

## 查明流程

以下六步法为域外法查明的标准操作流程。严格按顺序执行，每一步的输出作为下一步的输入。

### 步骤一：识别法域 (Jurisdiction Identification)

**目标**：准确确定待查明法律所属的国家或地区。

**操作要点：**

1. 根据用户问题，明确目标国家/地区的完整名称。
2. 识别目标法域所属的法系（普通法系/大陆法系/混合法系/宗教法系），这直接影响后续的法律渊源识别。
3. 注意以下特殊情形：
   - **联邦制国家**（美国、加拿大、澳大利亚、德国等）：区分联邦法和州/省法。联邦法律和州法律可能同时适用。
   - **特别行政区**（香港、澳门）：拥有独立的法律体系，与内地法律不同。
   - **海外属地**：部分国家的海外属地（如英属维尔京群岛、开曼群岛等）可能适用不同于宗主国的法律。
   - **欧盟成员国**：需同时考虑欧盟法（法规Regulation/指令Directive）和成员国国内法两个层级。
4. 明确时间维度：用户关注的是现行法律还是特定历史时期的法律。

**输出**：目标法域名称、法系归属、是否存在联邦/多层级法律体系。

### 步骤二：识别该法域的法律渊源 (Sources of Law)

**目标**：厘清目标法域的法律渊源类型及其位阶关系。

**操作要点：**

普通法系法域（典型：美国、英国、加拿大、澳大利亚、新加坡、香港）：

| 法律渊源 | 说明 |
|----------|------|
| 宪法/基本法 | 最高位阶，所有法律不得违宪 |
| 成文法/法规 (Statutes/Acts) | 立法机关制定的法律 |
| 授权立法/附属法规 (Delegated Legislation/Subsidiary Legislation) | 行政机关依授权制定的法规 |
| 判例法 (Case Law) | 法院判决构成具有约束力的先例（遵循 stare decisis 原则） |
| 习惯法 (Customary Law) | 部分法域承认习惯法的效力 |

大陆法系法域（典型：法国、德国、日本、韩国、中国台湾）：

| 法律渊源 | 说明 |
|----------|------|
| 宪法 | 最高位阶 |
| 法典 (Codes) | 系统化的成文法典（民法典、刑法典、商法典等） |
| 单行法/特别法 | 针对特定领域的法律 |
| 行政法规/行政命令 | 行政机关发布的法规 |
| 判例 | 不构成正式法源，但具有重要参考价值（法理上的事实约束力） |

**输出**：目标法域的法律渊源类型、位阶关系、各法源的约束力判断标准。

### 步骤三：识别具体的法律法规名称 (Identify Specific Legal Instruments)

**目标**：根据用户问题涉及的领域，匹配目标法域中对应的具体法律法规。

**操作要点：**

1. 将用户问题归类到法律部门（如：公司法、合同法、知识产权法、数据保护法、劳动法、税法、反垄断法、环境法等）。
2. 在目标法域中定位对应法律：
   - 利用 `references/数据库索引.md` 找到该法域的官方立法数据库
   - 在数据库中按部门法分类或关键词搜索
3. 对于普通法系法域，同时识别：
   - 相关成文法的完整名称（含年份）
   - 可能需要查明的关键判例（landmark cases）
4. 对于大陆法系法域，同时识别：
   - 相关法典的具体卷/编/章
   - 相关的特别法/单行法
5. 注意确认法律的最新修订状态：检索时应确认是否为现行有效版本。

**常见部门法与典型法域对照（参考）：**

| 法律领域 | 美国 | 英国 | 欧盟 | 日本 | 新加坡 |
|----------|------|------|------|------|--------|
| 公司法 | Delaware General Corporation Law; Model Business Corporation Act | Companies Act 2006 | EU Company Law Directives | 会社法 (Companies Act) | Companies Act (Cap. 50) |
| 数据保护 | CCPA (加州); various state laws | UK GDPR; Data Protection Act 2018 | GDPR | 個人情報保護法 | Personal Data Protection Act 2012 |
| 知识产权 | Lanham Act; Copyright Act; Patent Act | Copyright, Designs and Patents Act 1988 | EU IP Directives | 著作権法; 特許法; 商標法 | Copyright Act; Patents Act; Trade Marks Act |

**输出**：目标法律的完整名称（含年份）、最新修订版本、与该法律相关的关键判例或配套法规。

### 步骤四：定位具体规则 (Locate Specific Rules)

**目标**：在确定的法律文本中检索并提取适用于用户问题的具体法律条文。

**操作要点：**

1. 进入目标数据库（优先官方来源），定位目标法律文本。
2. 使用以下方法之一定位具体法条：
   - 按法条编号（section/article number）直接定位
   - 按关键词搜索法律文本全文
   - 使用数据库提供的高级检索功能（如按主题、按部门等）
3. 对于判例法法域，同时检索相关判例：
   - 查找成文法关键条款的司法解释
   - 检索法院对类似事实的判决
   - 使用判例引证系统（如 Shepard's、KeyCite 等的免费替代方案）
4. 注意提取以下完整信息：
   - 法条的完整原文（含上下文前后的关联条款）
   - 该法条的生效日期和最后修订日期
   - 是否存在过渡期条款或例外情形

**输出**：具体法条原文、所在章节、适用条件、但书/例外条款。

### 步骤五：质量审查 — 指出可能的错误点 (Quality Assurance)

**目标**：对查明的法律结果进行多维度的可靠性审查，主动识别并标注潜在问题。

**操作要点：**

逐项检查以下风险点，并在结果中明确标注：

1. **语言翻译风险**：
   - 法律术语在不同法系中可能有不同的内涵（如 "consideration" 在普通法合同法中的特殊含义）
   - 非英语国家法律的英文翻译可能存在不准确之处
   - 建议优先参考原始语言版本，英文翻译仅作辅助

2. **法律效力风险**：
   - 确认法条是否已被废止 (repealed) 或被新法取代 (superseded)
   - 确认法条是否被宪法或上级法律推翻 (struck down as unconstitutional)
   - 确认判例是否被后续判决推翻 (overruled) 或在特定情形下被限缩 (distinguished)
   - 确认法律是否尚未生效 (not yet in force)

3. **法律冲突风险**：
   - 联邦制国家：联邦法与州法之间是否存在冲突（如美国联邦法和加州法）
   - 欧盟成员国：欧盟法是否优先于国内法（supremacy of EU law）
   - 不同法律渊源之间是否存在矛盾

4. **适用范围风险**：
   - 确认存在但书条款 (proviso/saving clause) 或豁免条款 (exemption)
   - 确认法律是否有域外适用范围 (extraterritorial application)
   - 确认是否有过渡期安排 (transitional provisions)
   - 确认特定行业或主体的例外规定

5. **时效性风险**：
   - 法律文本是否为最新版本
   - 数据库是否有更新延迟（LII系列网站通常有数天至数周延迟）
   - 是否有已通过但尚未生效的修正案 (pending amendments)

**输出**：对每一项查明结果标注可靠性等级，逐一列出已检查的风险点和仍存在的不确定性。

### 步骤六：输出信息来源 (Source Citation)

**目标**：为每一项法律查明结果附上完整的、可验证的来源信息。

**操作要点：**

输出格式应包含以下要素（按类型区分）：

**对于成文法：**
```
- 法域：[国家/地区]
- 法律名称：[完整的官方名称]
- 法条编号：[Section/Article/§ + 编号]
- 来源数据库：[数据库名称 + URL]
- 版本信息：[生效日期/修订日期]
- 检索路径：[具体检索步骤，便于他人复现]
- 语言：[原文语言/是否有英文翻译]
```

**对于判例法：**
```
- 法域：[国家/地区]
- 案件名称：[Plaintiff v. Defendant]
- 案号/引证号：[Citation/案号]
- 判决法院：[法院名称 + 层级]
- 判决日期：[YYYY-MM-DD]
- 来源数据库：[数据库名称 + URL]
- 裁判要点：[Holding/Ratio Decidendi 简要概括]
```

**对于国际条约：**
```
- 条约名称：[完整名称]
- 签署/生效日期：[YYYY-MM-DD]
- 来源数据库：[数据库名称 + URL]
- 缔约国状态：[是否生效/中国是否加入]
- 相关条款：[Article + 编号]
```

**输出**：完整的来源引用清单，每条引用应可独立供第三方验证。

---

## 可选步骤：中国比较法视角

当用户明确要求进行中外法律比较时，执行此附加步骤。

**操作要点：**

1. 在中国法律体系中定位对应领域的法律规定（如民法典、刑法、公司法、个人信息保护法等）。
2. 从以下维度进行比较分析：
   - 立法体例差异（法典化 vs 单行法 vs 判例法）
   - 核心规则异同
   - 法律概念的可对应性（概念名称相同但内涵不同时须重点说明）
   - 适用范围和例外情形的差异
3. 指出实务中最常见的法律适用差异和合规要点。
4. 中性客观地呈现，不评价孰优孰劣。

---

## 数据库快速导航

以下为常用法域的首选数据库快速参考。完整列表见 `references/数据库索引.md`。

### 综合入口（多法域检索）
- **WorldLII** [worldlii.org](https://www.worldlii.org) — 120+ 法域一站式查询
- **GlobaLex (NYU)** [nyulawglobal.org/globalex](https://www.nyulawglobal.org/globalex/) — 各国法律体系概述和研究指南
- **Law Library of Congress** [guides.loc.gov/law-online](https://guides.loc.gov/law-online) — 全球法律资源权威导航

### 英美法系
- **美国**: Cornell LII [law.cornell.edu](https://www.law.cornell.edu) / GovInfo [govinfo.gov](https://www.govinfo.gov) / Caselaw Access Project [case.law](https://case.law)
- **英国**: Legislation.gov.uk [legislation.gov.uk](https://www.legislation.gov.uk) / BAILII [bailii.org](https://www.bailii.org)
- **加拿大**: CanLII [canlii.org](https://www.canlii.org)
- **澳大利亚**: AustLII [austlii.edu.au](https://www.austlii.edu.au)
- **新加坡**: Singapore Statutes Online [sso.agc.gov.sg](https://sso.agc.gov.sg)
- **香港**: Hong Kong e-Legislation [elegislation.gov.hk](https://www.elegislation.gov.hk) / HKLII [hklii.hk](https://www.hklii.hk)

### 欧盟法
- **EUR-Lex** [eur-lex.europa.eu](https://eur-lex.europa.eu) — 欧盟法规/指令/判例的权威来源
- **CURIA** [curia.europa.eu](https://curia.europa.eu) — 欧盟法院判例
- **HUDOC** [hudoc.echr.coe.int](https://hudoc.echr.coe.int) — 欧洲人权法院判例

### 大陆法系欧洲
- **法国**: Legifrance [legifrance.gouv.fr](https://www.legifrance.gouv.fr)
- **德国**: Gesetze im Internet [gesetze-im-internet.de](https://www.gesetze-im-internet.de)
- **瑞士**: Fedlex [fedlex.admin.ch](https://www.fedlex.admin.ch)
- **意大利**: Normattiva [normattiva.it](https://www.normattiva.it)
- **西班牙**: BOE.es [boe.es](https://www.boe.es)
- **荷兰**: Overheid.nl [wetten.overheid.nl](https://wetten.overheid.nl)

### 亚洲
- **日本**: Japanese Law Translation [japaneselawtranslation.go.jp](https://www.japaneselawtranslation.go.jp)
- **韩国**: KLRI e-Law [elaw.klri.re.kr/eng_service/main.do](https://elaw.klri.re.kr/eng_service/main.do)
- **台湾**: Laws & Regulations DB [law.moj.gov.tw/eng](https://law.moj.gov.tw/eng/)

### 国际条约与专题
- **UN Treaty Collection** [treaties.un.org](https://treaties.un.org)
- **HCCH 海牙国际私法** [hcch.net](https://www.hcch.net)
- **WIPO Lex 知识产权** [wipo.int/wipolex/en](https://www.wipo.int/wipolex/en/)
- **NATLEX 劳动法** [ilo.org/dyn/natlex](https://www.ilo.org/dyn/natlex/natlex4.home)
- **WTO 贸易法** [docs.wto.org](https://docs.wto.org)

---

## 使用注意事项

### 网络访问（中国大陆环境）
- 大多数国际组织网站（UN、EU、WTO）可正常访问
- Google Scholar `scholar.google.com` 访问不稳定，查找美国判例时应优先使用 CourtListener 或 Caselaw Access Project
- 俄罗斯 `pravo.gov.ru` 可能不稳定

### 权威性优先级
始终按以下优先级选择数据源：
1. 官方政府网站或国际组织官方网站（🟢 标记）—— 法律文本的官方来源
2. LII/学术机构网站（🟡 标记）—— 数据质量高，交叉验证用
3. 第三方平台（🔵 标记）—— 仅作辅助参考，须与官方数据交叉核对

### 语言处理策略
1. 对于使用非中文官方语言的搜索结果，提供原文后附中文翻译（标注"非官方翻译，仅供参考"）
2. 对于非英语法域（日本、韩国、法国、德国等），优先使用官方英文翻译版本（如有）
3. 法律术语翻译需标注原文对应词，避免望文生义
4. 重要法律术语在首次出现时提供双语对照

### 爬虫合规
- 大规模批量下载前，务必查阅目标网站的 robots.txt 和 Terms of Use
- 推荐爬取间隔：至少 3-5 秒
- 所有引用须标注数据来源

---

## 参考资料

- **`references/数据库索引.md`** — 完整的 121 个数据库索引，按法域和专题归类。在确定法域后务必查阅此文件选择最佳数据源。
