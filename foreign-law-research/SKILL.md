---
name: foreign-law-research
description: This skill should be used when the user asks to research, ascertain, or verify foreign or overseas laws — including "foreign law ascertainment", "ascertain the law of [country]", "overseas law research", "comparative law research", "what does [country] law say about…", "is [statute/case] still in force", point-in-time law lookup, or any request about specific legal provisions in jurisdictions outside mainland China (US, UK, EU, Japan, South Korea, Singapore, Hong Kong, Australia, Canada, Germany, France, etc.). Also trigger on Chinese phrasings such as "域外法", "外国法", "海外法律", "比较法", "外国法律查明", "域外法律研究", "涉外法律", "查明某国法律", "外国法律查明意见书". The skill produces traceable, verifiable research results aligned with the standards PRC courts apply when ascertaining foreign law, delivered as a formal Ascertainment Opinion plus a Research Log.
version: 2.0.0
---

# Foreign Law Research & Ascertainment Skill

This skill guides lawyers and legal professionals through the systematic ascertainment of foreign law (statutes, case law, and international treaties of any jurisdiction outside mainland China). Version 2.0 aligns the whole workflow with the evidentiary standards applied by PRC courts — modeled on the Shanghai Financial Court's *Guidelines on the Ascertainment of Foreign Law* (2025) and the SPC judicial interpretations of the Law on the Application of Laws to Foreign-Related Civil Relations — so that research output is **ready for submission and cross-examination in court**: an *Ascertainment Opinion* plus a *Research Log*.

Data layer: **121 free legal databases** plus an **open-source data layer** (git-versioned law corpora, open legal data collection scripts, and MCP servers).

## Overview

Ascertaining foreign law is more than "finding the provision". In PRC cross-border practice, an ascertainment result must survive cross-examination and judicial review (Guidelines Art. 14): authenticity of the text, validity status, relevance to the dispute, and completeness of the search. This skill organizes the work as **Scoping → Six research steps → Dual deliverables**:

```
Step 0  Scoping ───────────┐
Step 1  Identify jurisdiction │
Step 2  Map sources of law    │  Research
Step 3  Identify instruments  │  (log as you go)
Step 4  Locate specific rules │
Step 5  Quality assurance ───┘
Step 6  Deliver ──→ Ascertainment Opinion (six-part structure)
                 Research Log (search audit trail)
                 AI-tool disclosure (tools / stages / human verification)
```

## Reference map

Four reference files support the workflow. Consult them on demand:

| File | Purpose | When to read |
|------|---------|--------------|
| `references/database-index.md` | 121 free legal databases by jurisdiction, three authority tiers | After Step 1, to pick research databases |
| `references/open-source-data.md` | Open-source data layer: git law corpora, collection scripts, MCP servers | When you need version history, validity verification, bulk endpoints, or a jurisdiction covered by an MCP |
| `references/opinion-template.md` | Fill-in skeleton of the six-part Ascertainment Opinion | At Step 6, when producing the final opinion |
| `references/research-log-template.md` | Search audit-trail table | Open it when research begins; deliver it with the opinion at Step 6 |

**Mandatory practice: start every engagement by opening a Research Log.** Record every search action (database, query, hits, verification) as you go, and deliver the log alongside the opinion. The log is the core evidence courts use to review the ascertainment process (Guidelines Art. 12) and the answer to "was the search method reliable" challenges (Art. 14).

---

## The nine ascertainment channels

This skill covers the AI-assisted research channel. Under Guidelines Art. 5, foreign law may be ascertained through nine channels; AI research is only one of them. When reliability is insufficient or stronger probative force is needed, recommend combining channels:

| # | Channel | This skill's role |
|---|---------|-------------------|
| 1 | Provided by a party (own research / hired expert / ascertainment agency) | ✅ This skill serves this channel: producing draft ascertainment output for the party or its expert |
| 2 | Judicial assistance (central/competent authority of the foreign state) | Flag as available on request |
| 3 | Via embassies/consulates (through the SPC) | Flag as available on request |
| 4 | SPC-established or -participating ascertainment cooperation mechanisms | Flag as available on request |
| 5 | Experts of the SPC International Commercial Expert Committee | Flag as available on request |
| 6 | Legal ascertainment service agencies / legal experts (judges, lawyers, scholars) | Recommend as the verifying and signing entity for AI output |
| 7 | PRC judgments that already ascertained the same or similar foreign law | ✅ Search China Judgments Online etc. as corroboration (re-verify current validity — Art. 19) |
| 8 | The court's own research | ✅ This skill's methodology applies directly |
| 9 | Other appropriate channels | — |

**Practice note**: AI research output counts as "provided by a party" or assists "the court's own research". For court submission it normally requires review and signature by a qualified expert of the target jurisdiction (Art. 6: locally licensed lawyers, scholars in the relevant field, etc.; Art. 11: signature rules) plus disclosure of AI-tool use (Art. 10). The opinion template bakes in both.

---

## Workflow

### Step 0: Scoping

**Goal**: Fix the scope of ascertainment before any searching. Mirrors the pre-trial scoping items of Guidelines Art. 4.

**Key actions:**

1. Confirm the following six items with the user and record each (if information is missing, **ask before searching** — never start with a fuzzy scope):
   - **Legal disputes and applicable law**: which legal relationship, which jurisdiction's law governs (party choice? conflict-of-laws rule?)
   - **Established or undisputed facts**: ascertainment must connect to facts; a context-free list of provisions has no probative value
   - **List of legal questions to be ascertained**: decompose into specific, answerable questions (e.g., "formal requirements for a guarantee contract under Singapore law", not "Singapore guarantee law")
   - **Channels and division of labor**: this skill handles AI research; flag expert/agency channels as needed
   - **Timing**: PRC courts generally give parties no more than 60 days to provide foreign law (extendable) — plan the research backwards from the deadline
   - **Budget constraints**: free sources only, or are paid services allowed?
2. Produce a **Scope Memorandum** as the anchor for all later steps; update it (with reasons) whenever the scope changes.

**Output**: Scope Memorandum (disputes — governing law — factual premises — question list — channels — deadline).

### Step 1: Identify the Jurisdiction

**Goal**: Pin down the country or legal system whose law is to be ascertained.

**Key actions:**

1. From the Scope Memorandum, name the target country/region precisely.
2. Identify its legal family (common law / civil law / mixed / religious) — this drives source-of-law analysis.
3. Watch for special situations:
   - **Federal states** (US, Canada, Australia, Germany…): distinguish federal law from state/provincial law; both may apply simultaneously.
   - **Special administrative regions** (Hong Kong, Macau): independent legal systems distinct from mainland China.
   - **Overseas territories**: some (BVI, Cayman, …) follow law different from the metropolitan state.
   - **EU member states**: consider EU law (Regulations/Directives) and national law as two layers.
4. Fix the temporal dimension: **current law, or the law as of a historical date** (contract conclusion, tort occurrence). Record historical-version questions in the Research Log; verify with versioned tools at Step 4.
5. **Extended scope** (Guidelines Art. 24): ascertainment of the law of Hong Kong, Macau and Taiwan follows this workflow mutatis mutandis; so do international treaties, international organization rules, and international customs.

**Output**: Jurisdiction name, legal family, federal/multi-layer structure, temporal reference date.

### Step 2: Map the Sources of Law

**Goal**: Identify the types of legal sources in the target jurisdiction and their hierarchy.

**Key actions:**

Common-law jurisdictions (US, UK, Canada, Australia, Singapore, Hong Kong…):

| Source | Notes |
|--------|-------|
| Constitution / Basic Law | Supreme rank; no law may contradict it |
| Statutes / Acts | Enacted by the legislature |
| Delegated / subsidiary legislation | Made by the executive under authorization |
| Case law | Binding precedent under stare decisis |
| Customary law | Recognized in some jurisdictions |

Civil-law jurisdictions (France, Germany, Japan, South Korea, Taiwan…):

| Source | Notes |
|--------|-------|
| Constitution | Supreme rank |
| Codes | Systematized codes (civil, criminal, commercial…) |
| Special / single statutes | Domain-specific legislation |
| Administrative regulations | Executive rulemaking |
| Case law | Not a formal source but highly persuasive (de facto authority) |

**Position of auxiliary materials** (Guidelines Art. 1): legal doctrine, legislative preparatory materials, case commentary, and industry practice are not law itself but may be submitted as reference materials for understanding and interpreting foreign law. When cited in the opinion, always label them as auxiliary and distinguish them from binding sources.

**Output**: Source types, hierarchy, and the test for each source's binding force.

### Step 3: Identify Specific Legal Instruments

**Goal**: Map each legal question from the Scope Memorandum to the specific instruments of the target jurisdiction.

**Key actions:**

1. Classify each question by legal field (company, contract, IP, data protection, employment, tax, antitrust, environmental…).
2. Locate the corresponding law:
   - Use `references/database-index.md` to find the jurisdiction's official legislative database
   - Search by field classification or keywords
   - If the jurisdiction has MCP coverage or an open corpus, check the coverage matrix in `references/open-source-data.md` first
3. For common-law jurisdictions, also identify:
   - Full names of relevant statutes (with year)
   - Key precedents (landmark cases) likely to be ascertained
4. For civil-law jurisdictions, also identify:
   - The specific books/parts/chapters of codes
   - Related special statutes
5. Confirm the current amendment status of each instrument.

**Reference mapping of common fields:**

| Field | US | UK | EU | Japan | Singapore |
|-------|----|----|----|-------|-----------|
| Company | Delaware GCC; MBCA | Companies Act 2006 | EU Company Law Directives | 会社法 (Companies Act) | Companies Act (Cap. 50) |
| Data protection | CCPA (CA); state laws | UK GDPR; DPA 2018 | GDPR | 個人情報保護法 | PDPA 2012 |
| IP | Lanham Act; Copyright Act; Patent Act | CDPA 1988 | EU IP Directives | 著作権法; 特許法; 商標法 | Copyright Act; Patents Act; Trade Marks Act |

**Output**: Full instrument names (with years), latest amendment versions, related key cases and ancillary regulations.

### Step 4: Locate Specific Rules

**Goal**: Retrieve and extract the specific rules bearing on each legal question.

**Key actions:**

1. Enter the target database (official sources first) and locate the instrument text.
2. Locate provisions by one of:
   - Direct citation (section/article number)
   - Full-text keyword search
   - Advanced search (by topic, field…)
3. **Citation resolution**: for case citations (ECLI, US reporter citations, German Aktenzeichen, French pourvoi numbers, Swiss BGE…) or abbreviated statutory citations (§ 823 BGB, art. 1240 code civil…), resolve via lexifina's citation tools (see `references/open-source-data.md`) or the official database.
4. **Point-in-time law**: where the Scope Memorandum fixes a historical reference date, verify the text in force on that date with lexifina's `law.py show <date> <path>` or `law.py diff`; absent tooling, consult the official database's revision history.
5. For case-law jurisdictions, also search case law:
   - Judicial interpretations of key statutory provisions
   - Decisions on analogous facts
   - Free citator alternatives to Shepard's/KeyCite
6. Extract complete information:
   - Full text of the provision (with surrounding context)
   - Entry-into-force date and last amendment date
   - Transitional provisions or exceptions
7. **Log every search action** in the Research Log (database/tool, query or keywords, hits, and failed attempts).

**Output**: Provision text, location, conditions of application, provisos/exceptions, holdings of key cases.

### Step 5: Quality Assurance

**Goal**: Multi-dimensional reliability review. This step maps directly onto what opposing parties and the court will examine (Guidelines Art. 14). Only reviewed results enter the opinion.

**Key actions:**

**A. Validity verification** (Guidelines Art. 10(4) — mandatory for every source):

1. Confirm **entry into force**, amendment history, whether **repealed** or **superseded**
2. Confirm whether **struck down** as unconstitutional or ultra vires
3. For precedents: **overruled**, **distinguished/narrowed**, or still **good law**
4. Confirm whether **not yet in force**, and any **pending amendments**
5. For federal states, state the **level and scope** (federal/state); for EU members, distinguish EU law from national law
6. Verify with lexifina's point-in-time / precedent-check tools first, then official revision records

**B. Five-point cross-examination self-check** (Guidelines Art. 14 — run before every delivery and address in the opinion):

| # | Examination point | Self-check action |
|---|------------------|-------------------|
| 1 | Authenticity of text & accuracy of translation | Check against official source; label translations "unofficial, for reference only"; annotate terms with original wording |
| 2 | Validity status | Complete part A in full |
| 3 | Relevance, application, retroactivity | Map each question to specific provisions/cases; check retroactivity clauses |
| 4 | Completeness | Cover synonyms and adjacent fields; **search for and disclose contrary provisions and cases** (Art. 7 prohibits concealment) |
| 5 | Authority of sources | Tag every source (🟢/🟡/🔵); third-party sources require cross-verification against official ones |

**C. Residual risks** (carried over from v1):

1. **Translation risk**: terms shift meaning across legal families (e.g., "consideration"); non-English official texts — prefer the original
2. **Conflict risk**: federal vs state conflicts; supremacy of EU law
3. **Timeliness risk**: database lag (LII sites typically days to weeks old); adopted-but-not-in-force amendments

**Output**: Reliability rating per finding, list of checked risks, remaining uncertainties (feed into the opinion).

### Step 6: Deliver the Dual Deliverables

**Goal**: Produce the two documents to judicial evidentiary standard. **Take the skeletons from `references/opinion-template.md` and `references/research-log-template.md` — do not improvise structure.**

**Deliverable 1: Ascertainment Opinion** — six-part structure (Guidelines Art. 10):

1. **Matters ascertained** — target jurisdiction + the specific disputes (from the Step 0 Scope Memorandum)
2. **Factual premises and assumptions** — documents relied on, known facts, evidence, necessary assumptions; where facts are disputed, state the legal consequences under each version
3. **Channels and sources** — how and when the law was retrieved, databases/tools used, authority/reliability/timeliness of each source
4. **Legal provisions and their validity** — full texts of statutes, cases, or other sources, with effect dates and amendment/repeal status; for federal/multi-jurisdiction states, the level and scope
5. **Interpretation and application** — how the jurisdiction's courts ordinarily understand and apply the rules; mapping to the facts of the case; for each cited case, its validity status, binding force, similarities/differences and persuasive value
6. **Conclusions** — answer every ascertained question specifically; disclose divergent interpretations, case conflicts, or uncertainties with each view's basis and consequences

Attachments: original-language texts plus accurate Chinese translations; full text of cited cases in case-law jurisdictions.

**Deliverable 2: Research Log** (Guidelines Art. 12): search times, paths and keywords, texts obtained, and validity-verification results.

**AI-tool disclosure (mandatory, Art. 10 final ¶)**: where AI tools assisted retrieval or translation, the opinion must disclose:
- Tool names (this skill + specific databases/MCP/search tools)
- Stages of use (search / translation / comparison / drafting)
- Human verification of the affected content (what was verified, how, what was not)

> Failure to disclose — or inaccurate disclosure — may trigger court sanctions and directly reduces the probative weight of the opinion.

**Signature note** (Art. 11): for judicial submission the opinion must be signed by the responsible expert (agency ascertained: agency seal; multiple experts: division of labor + all signatures). Recommend review and signature by an expert qualified under Art. 6.

---

## Open-source data layer (quick view)

Beyond the 121 web databases, v2.0 adds an open-source data layer. Full usage, coverage matrix and setup commands: `references/open-source-data.md`:

| Source | Type | Core value | Typical use |
|--------|------|-----------|-------------|
| 🟣 [lexifina/global-law](https://github.com/lexifina/global-law) | git-versioned law corpora (CC0) | Law on any date, per-word provenance, case law for US/DE/FR/CH/NL/PL/FI/AT, citation resolution | Step 4 point-in-time lookup; Step 5 validity verification |
| ⚙️ [worldwidelaw/legal-sources](https://github.com/worldwidelaw/legal-sources) | Open data collection scripts | Official endpoints catalog for 110+ countries + search API over 16M documents | Locating a country's official bulk/API entry; supplementary discovery |
| 🔌 [Ansvar Gateway](https://ansvar.eu/docs/quickstart) | MCP server fleet | One endpoint covering 28 jurisdictions' national law + EU law + financial-regulation/data-protection/cybersecurity corpora, verbatim citations | Structured retrieval for European + EU jurisdictions |
| 🔌 lexifina local MCP | MCP (offline) | 18 read-only tools: find, point-in-time read, blame, diff, precedent check | Local retrieval on a cloned corpus |

**Priority unchanged**: official > open-source mirror/LII > third-party. The open layer is for **verification and deep dives**, not a substitute for final confirmation against official sources.

---

## Database quick navigation

First-choice databases for common jurisdictions. Full list: `references/database-index.md`.

### Multi-jurisdiction gateways
- **WorldLII** [worldlii.org](https://www.worldlii.org) — one-stop search across 120+ jurisdictions
- **GlobaLex (NYU)** [nyulawglobal.org/globalex](https://www.nyulawglobal.org/globalex/) — legal system overviews and research guides per country
- **Law Library of Congress** [guides.loc.gov/law-online](https://guides.loc.gov/law-online) — authoritative global navigation

### Common law
- **US**: Cornell LII [law.cornell.edu](https://www.law.cornell.edu) / GovInfo [govinfo.gov](https://www.govinfo.gov) / Caselaw Access Project [case.law](https://case.law)
- **UK**: Legislation.gov.uk [legislation.gov.uk](https://www.legislation.gov.uk) / BAILII [bailii.org](https://www.bailii.org)
- **Canada**: CanLII [canlii.org](https://www.canlii.org)
- **Australia**: AustLII [austlii.edu.au](https://www.austlii.edu.au)
- **Singapore**: Singapore Statutes Online [sso.agc.gov.sg](https://sso.agc.gov.sg)
- **Hong Kong**: Hong Kong e-Legislation [elegislation.gov.hk](https://www.elegislation.gov.hk) / HKLII [hklii.hk](https://www.hklii.hk)

### EU law
- **EUR-Lex** [eur-lex.europa.eu](https://eur-lex.europa.eu) — authoritative source for EU regulations/directives/case law
- **CURIA** [curia.europa.eu](https://curia.europa.eu) — CJEU case law
- **HUDOC** [hudoc.echr.coe.int](https://hudoc.echr.coe.int) — ECtHR case law

### Civil-law Europe
- **France**: Legifrance [legifrance.gouv.fr](https://www.legifrance.gouv.fr)
- **Germany**: Gesetze im Internet [gesetze-im-internet.de](https://www.gesetze-im-internet.de)
- **Switzerland**: Fedlex [fedlex.admin.ch](https://www.fedlex.admin.ch)
- **Italy**: Normattiva [normattiva.it](https://www.normattiva.it)
- **Spain**: BOE.es [boe.es](https://www.boe.es)
- **Netherlands**: Overheid.nl [wetten.overheid.nl](https://wetten.overheid.nl)

### Asia
- **Japan**: Japanese Law Translation [japaneselawtranslation.go.jp](https://www.japaneselawtranslation.go.jp)
- **South Korea**: KLRI e-Law [elaw.klri.re.kr/eng_service/main.do](https://elaw.klri.re.kr/eng_service/main.do)
- **Taiwan**: Laws & Regulations DB [law.moj.gov.tw/eng](https://law.moj.gov.tw/eng/)

### Treaties & subjects
- **UN Treaty Collection** [treaties.un.org](https://treaties.un.org)
- **HCCH** [hcch.net](https://www.hcch.net)
- **WIPO Lex** [wipo.int/wipolex/en](https://www.wipo.int/wipolex/en/)
- **NATLEX (labor)** [ilo.org/dyn/natlex](https://www.ilo.org/dyn/natlex/natlex4.home)
- **WTO** [docs.wto.org](https://docs.wto.org)

### PRC corroboration
- **China Judgments Online / SPC Case Database** — search PRC judgments that already ascertained the same or similar foreign-law issues (Art. 5(7), Art. 19); re-verify the foreign law's current validity before relying on them

---

## When foreign law cannot be ascertained

When reasonable channels are exhausted without result, or what is obtained is unclear or insufficient (Guidelines Art. 20), **tell the user honestly** — never fabricate or fill gaps with speculation:

1. Standard: not obtainable through reasonable channels (party provision, treaty channels, experts/agencies…); or the party chose foreign law but failed to provide it without justification within the deadline
2. Consequence: where foreign law cannot be ascertained or provides no rule, PRC law applies (Art. 21; Law on the Application of Laws, Art. 10)
3. Output: list the attempted channels (in the Research Log), reasons for failure, recommended next channels (ascertainment agency, judicial assistance), and flag the possibility of PRC law applying
4. Partial ascertainment: separate what was ascertained from what was not; handle each accordingly

---

## Optional step: PRC comparative-law perspective

Run this step only when the user expressly asks for China–foreign comparison.

**Key actions:**

1. Locate the corresponding PRC rules (Civil Code, Company Law, PIPL, etc.).
2. Compare along: legislative technique (codes vs single statutes vs case law); core rule differences; conceptual commensurability (flag same-name-different-content concepts); scope and exceptions.
3. Highlight practical divergences and compliance points.
4. Present neutrally — no value ranking of legal systems.

---

## Practical notes

### Network access
- Most international organization sites (UN, EU, WTO) are reachable
- Google Scholar is unstable from mainland China — prefer CourtListener or Caselaw Access Project for US cases
- `pravo.gov.ru` may be unstable
- Cloning the open-source layer from GitHub may require a proxy from mainland China

### Authority priority
1. Official government / international organization sites (🟢) — the authoritative text
2. Open-source versioned corpora (🟣) — verification and historical versions; final confirmation stays with official sources
3. LII / academic sites (🟡) — high quality; cross-verification
4. Third-party platforms (🔵) — auxiliary only; cross-check against official data

### Language policy
1. For non-Chinese sources, give the original text followed by a Chinese translation (labeled "unofficial translation, for reference only")
2. For non-English jurisdictions (JP, KR, FR, DE…), prefer official English translations when available
3. Annotate legal terms with the original wording — avoid false friends
4. Provide bilingual glosses for key terms on first occurrence

### Crawling compliance
- Check robots.txt and Terms of Use before bulk downloads
- Rate limit: at least 3–5 seconds between requests
- Attribute every source
- Respect per-script rate limits when running legal-sources collection scripts

### AI-tool discipline (Guidelines Arts. 7 & 10)
1. Be objective and neutral: search for and disclose contrary provisions and case law — no selective presentation
2. Truthfully describe search scope and method (that is what the Research Log is for)
3. AI results for judicial use must be human-verified by a qualified expert before submission
4. The opinion must contain the AI-tool disclosure block

---

## References

- **`references/database-index.md`** — the full 121-database index by jurisdiction and subject. Consult after fixing the jurisdiction.
- **`references/open-source-data.md`** — full guide to the open-source layer: lexifina/global-law, worldwidelaw/legal-sources, Ansvar MCP — coverage matrix, setup commands, licensing.
- **`references/opinion-template.md`** — six-part Ascertainment Opinion template + AI disclosure + signature blocks. Use at Step 6.
- **`references/research-log-template.md`** — search audit-trail template. Open at the start; deliver with the opinion.

## Methodology sources

- *Shanghai Financial Court Guidelines on the Ascertainment of Foreign Law* (2025) — primary framework: Step 0 (Art. 4), channels (Art. 5), opinion structure (Art. 10), research log (Art. 12), cross-examination points (Art. 14), non-ascertainment (Arts. 20–21), extended scope (Art. 24)
- PRC Law on the Application of Laws to Foreign-Related Civil Relations, Art. 10, and SPC Interpretations (I) & (II)
- README/documentation of the open-source repositories (see `references/open-source-data.md` for sources and licenses)
