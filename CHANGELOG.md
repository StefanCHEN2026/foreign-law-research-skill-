# Changelog

All notable changes to this project are documented in this file. Format follows [Keep a Changelog](https://keepachangelog.com/); versioning follows SemVer.

## [2.0.0] — 2026-11-07

A major upgrade: judicial-standards-aligned methodology, an open-source data layer, and a bilingual English edition.

### Added

- **Step 0: Scoping** (查明范围界定) — fix disputes, governing law, undisputed facts, question list, channels and deadlines before searching (Guidelines Art. 4); deliverable: Scope Memorandum.
- **Dual deliverables** replacing plain cited results:
  - *Ascertainment Opinion* (外国法律查明意见书) template in the six-part judicial format (Art. 10): matters ascertained; factual premises and assumptions; channels and sources; legal provisions and their validity; interpretation and application; conclusions — plus AI-tool disclosure, independence declaration, expert-signature and agency-seal blocks, and annex requirements (original text + Chinese translation, full case texts).
  - *Research Log* (外国法律查明工作记录) template (Art. 12): search journal, validity-verification table, contrary-authority searches, open items, AI-use summary.
- **AI-tool disclosure requirements** (Art. 10 final ¶): tool names, stages of use, human verification — with practice notes on sanctions for non-disclosure.
- **Five-point cross-examination self-check** (Art. 14) added to Quality Assurance: authenticity/translation, validity status, relevance/retroactivity, completeness (incl. mandatory disclosure of contrary authority, Art. 7), source authority.
- **Point-in-time validity verification**: statute effect/amendment/repeal checks and good-law checks for precedents, powered by the new open-source layer.
- **Nine ascertainment channels map** (Art. 5): positions AI-assisted research among party provision, judicial assistance, embassies, SPC mechanisms, expert committees, agencies, prior PRC judgments, and court research.
- **Non-ascertainment criteria** (Arts. 20–21): honest reporting when reasonable channels fail, with PRC-law fallback guidance.
- **Open-source data layer** (`references/开源数据源.md` / `open-source-data.md`):
  - 🟣 [lexifina/global-law](https://github.com/lexifina/global-law) — git-versioned law (one commit per law taking effect): law on any date, per-word provenance, case law for US/DE/FR/CH/NL/PL/FI/AT, citation resolution (ECLI, BGE, pourvoi, Aktenzeichen, §-shorthand), CLI + 18-tool local MCP (CC0).
  - ⚙️ [worldwidelaw/legal-sources](https://github.com/worldwidelaw/legal-sources) — 960+ collection scripts across 110+ countries as a catalog of official bulk/API endpoints; legaldatahunter.com search API over 16M+ documents.
  - 🔌 [Ansvar Systems](https://github.com/Ansvar-Systems) — MCP gateway `https://gateway.ansvar.eu/mcp`: 28 jurisdictions' national law + EU law + financial-regulation/data-protection/cybersecurity corpora, verbatim citations, free tier.
  - Selection matrix, setup commands, and license/attribution guidance.
- **English edition** (`foreign-law-research/`): full mirror skill with translated SKILL.md, database index (all 121 entries), open-source-data guide, and both templates. Bilingual trigger phrases in both SKILL.md frontmatters.
- Bilingual `README.md` and this `CHANGELOG.md`.

### Changed

- SKILL.md restructured around Scoping → Steps 1–6 → dual deliverables; version bumped to 2.0.0; description now includes English trigger phrases.
- Quality Assurance (Step 5) upgraded: mandatory validity-verification block; cross-examination self-check table; residual risk list retained.
- Step 4 adds citation resolution and point-in-time lookup workflows.
- Authority priority now includes the open-source tier: 🟢 official → 🟣 open versioned corpora → 🟡 LII/academic → 🔵 third-party.
- Database index header cross-references the open-source data layer.
- AI-tool discipline section added (objectivity, disclosure, human verification, expert countersignature).

### Compatibility

- Directory name `域外法查明/` and skill name unchanged — existing installations keep working after `git pull`.
- v1 six-step methodology remains recognizable inside the new workflow; v1 outputs remain valid as research notes, but court submissions should adopt the v2 opinion template.

## [1.0.0] — 2026-06-06

- Initial release: six-step foreign-law research methodology and an index of 121 free legal databases across 30+ jurisdictions, with three authority tiers, mainland-China accessibility notes, language policy, and crawling compliance guidance.
