# Open-Source Legal Data Sources Guide

> New in v2.0. This guide covers three open-source data layers: git-versioned law corpora, open legal data collection scripts, and MCP servers.
> Positioning: **verification and deep dives** — version checks, historical comparison, bulk-endpoint discovery, and structured retrieval. They do **not** replace final confirmation against official sources.
> Cloning from GitHub may require a proxy from mainland China.

---

## 1. Selection matrix: which one when

| Need | First choice | Notes |
|------|--------------|-------|
| Text of a provision on a specific historical date | 🟣 lexifina | Point-in-time: `law.py show <date> <path>` |
| Trace a provision's amendment/repeal history | 🟣 lexifina | `law.py blame` / `law.py diff` trace every change to the law that made it |
| Check whether a precedent is still good law | 🟣 lexifina `check_precedent` / official citators | Lists decisions applying a provision and whether the text each applied is still in force |
| Resolve citations (ECLI, BGE, pourvoi, Aktenzeichen, § shorthand) | 🟣 lexifina | `find_provision` / `law_details` / `resolve_citations` |
| Find a country's official bulk/API endpoint | ⚙️ legal-sources | `sources/{COUNTRY_CODE}/` directory is the catalog |
| Cross-jurisdiction keyword discovery | ⚙️ legaldatahunter API | Search over 16M+ indexed documents |
| Structured retrieval for European/EU jurisdictions (inside an AI assistant) | 🔌 Ansvar Gateway | One MCP endpoint, verbatim citations |
| Offline / privacy-sensitive research | 🔌 lexifina local MCP | Python 3.9+ and git only; zero network calls |
| General ascertainment | The 121 web databases in database-index.md | Official sources first |

---

## 2. 🟣 Git-versioned law corpora: lexifina/global-law

**Repository**: <https://github.com/lexifina/global-law> (index layer CC0; each country's texts live in `lexifina/<country>-law` under that repository's own terms)
**Idea**: one git repository per jurisdiction where **every commit is a law taking effect** — so the tools can answer "what was the law of any country on any date" and "which law wrote each word".

### Coverage

- **Legislation**: federal/national/state/municipal levels for many countries (e.g., `germany/bund/acts/`, `brazil/bahia/acts/`)
- **Case law** (one file and one commit per published decision, dated the day decided):
  - US: Supreme Court + courts of appeals (ca1–ca11, cadc, cafc), from the Caselaw Access Project (CC0)
  - Germany: BVerfG, BVwG, BFH, BAG, BPatG, filed by ECLI/Aktenzeichen
  - France: Cour de cassation, cours d'appel, Conseil d'État, Conseil constitutionnel (DILA open data, Licence Ouverte 2.0)
  - Switzerland: federal courts + cantonal courts
  - Netherlands: all court levels incl. the Hoge Raad, filed by ECLI
  - Poland: Supreme Court, Constitutional Tribunal etc. (SAOS; judgments outside copyright)
  - Finland (Finlex, CC BY 4.0), Austria (RIS, CC BY 4.0)
- **Citation resolution**: ECLI (`ECLI:NL:HR:2019:1234`), Swiss dockets (`4A_123/2024`), BGE references (`BGE 142 II 307`), French pourvoi (`n° 18-12.345`), QPC (`n° 2019-791 QPC`), DILA ids, German Aktenzeichen (`1 BvR 123/20`), and statutory shorthand (`§ 823 Abs. 1 BGB`, `§§ 280, 281 BGB`, `artikel 6:162 BW`, `article 1240 du code civil`, `Art. 336 OR`…)

### Setup and everyday commands

```bash
# Shallow-clone the index (no per-country history; small)
git clone --depth 1 https://github.com/lexifina/global-law && cd global-law

# Add corpora on demand (each country is several GB — do not add everything)
python3 tools/countries.py add united-states/federal/usc     # US Code
python3 tools/countries.py add germany/caselaw               # German case law
# Case-law corpora are NOT added with the country — add them separately

# Point-in-time: the provision in force on a date (use py/python on Windows)
python3 tools/law.py show 2022-05-01 united-states/federal/usc/title-11/1182.md
# Provenance: the law behind each line
python3 tools/law.py blame 2022-07-01 <path>
# Compare: what changed between two dates
python3 tools/law.py diff 2022-05-01 2022-07-01 <path>
# Laws that took effect in a window
python3 tools/law.py laws 1990-01-01 1990-12-31 germany
```

> ⚠️ Never `--depth`-clone an individual country repository — dates are read from its full history; `countries.py add` fetches all of it.

### MCP integration (18 read-only tools)

`tools/mcp_server.py` is a local MCP server (Python 3.9+ and git; makes no network calls). Tools include find_provision, read_law (provision on a date), words/blame, diff, check_precedent (precedent application + current validity), resolve_citations, search, and more. The clone ships configs for Claude Code, Cursor, VS Code and Codex — open the folder and the server starts. Other clients:

```json
{ "mcpServers": { "global-law": { "command": "git", "args": ["-C", "/path/to/global-law", "-c", "alias.global-law-mcp=!sh tools/mcp.sh", "global-law-mcp"] } } }
```

Full tool list: [MCP.md](https://github.com/lexifina/global-law/blob/main/MCP.md); corpus freshness: [FRESHNESS.md](https://github.com/lexifina/global-law/blob/main/FRESHNESS.md).

---

## 3. ⚙️ Open data collection scripts: worldwidelaw/legal-sources

**Repository**: <https://github.com/worldwidelaw/legal-sources> (open-source scripts; open-data positioning)
**Scale**: 110+ countries, 960+ collection scripts; dashboard & search API: <https://legaldatahunter.com> (16M+ indexed legal documents)

### Two ways to use it

**Way 1 — as a catalog of official endpoints (recommended; no code needed)**

The `sources/{COUNTRY_CODE}/{SourceName}/` tree *is* the answer: each subdirectory corresponds to one official portal/API/bulk endpoint; its `config.yaml` records the access method and rate limits, its `README.md` describes the source. When you need "where is country X's official data in bulk", browse that country's directory first.

```
sources/
  FR/LegifranceCodes/        # French consolidated codes (API)
  DE/GesetzeImInternet/      # German federal laws (bulk XML)
  IT/NormattivaLegislation/  # Italian legislation (API)
  ES/BOE/                    # Spanish official gazette (API)
  ...
```

**Way 2 — run the collection scripts (developer-oriented)**

```bash
git clone https://github.com/worldwidelaw/legal-sources.git && cd legal-sources
pip install -r requirements.txt
python runner.py status                      # project status
python runner.py sample FR/LegifranceCodes   # test one source (10+ sample docs)
```

Every script normalizes to a common schema (`_id/_source/_type[legislation|case_law]/title/text/date/url`), with two data models: **legislation** (mutable — upsert with version tracking) and **case law** (immutable — append-only with dedup).

**Coverage**: EU-27 130+ sources, EFTA/EEA 10+, Council-of-Europe countries 20+, Western Balkans 15+, Latin America 25+, Asia-Pacific 30+, Middle East & Africa 20+, others 15+.

**Search API**: legaldatahunter.com offers unified search over 16M+ documents — useful for cross-jurisdiction discovery (verify hits against official sources).

---

## 4. 🔌 MCP server fleet: Ansvar-Systems

**Organization**: <https://github.com/Ansvar-Systems> (maintained by Ansvar Systems, Stockholm; servers Apache-2.0; corpora hosted on their infrastructure)
**Scale**: 100 legal-MCP repositories, reachable through one gateway: **<https://gateway.ansvar.eu/mcp>** (OAuth signup, free tier; every result carries a verbatim source citation)

### Coverage

| Category | Coverage |
|----------|----------|
| National law (28 jurisdictions, mostly Europe) | UK, Germany, France, Italy, Spain, Portugal, Netherlands, Belgium, Luxembourg, Ireland, Austria, Switzerland, Poland, Czechia, Slovakia, Hungary, Romania, Bulgaria, Croatia, Slovenia, Estonia, Latvia, Lithuania, Finland, Sweden, Denmark, Iceland, Malta, Liechtenstein… |
| EU law | comprehensive-eu-law-mcp, EU_compliance_MCP |
| Domain corpora (per country) | Financial regulation (14 countries), data protection (20+ countries), cybersecurity (14 countries), healthcare, critical infrastructure, supply-chain security, German competition law… |

### Connect (one line)

```bash
# Claude Code
claude mcp add ansvar --transport http https://gateway.ansvar.eu/mcp
```

```json
// Claude Desktop / Cursor / generic MCP clients
{ "mcpServers": { "ansvar": { "type": "url", "url": "https://gateway.ansvar.eu/mcp" } } }
```

The first request opens an OAuth signup flow (quickstart: <https://ansvar.eu/docs/quickstart>); the tier (free/premium/team/company) sets quota and reachable downstream MCPs.

> ⚠️ The corpora are **not redistributed** in the repositories (upstream TDM and standards-licensing constraints); each repo ships ingestion scripts to build your own. Using the gateway means accepting its terms of service; for judicial use, still verify key provisions against the official gazette.

---

## 5. Sources, licenses, and attribution

| Source | Index/tools license | Data license |
|--------|---------------------|--------------|
| lexifina/global-law | CC0 | Per-country repository terms (e.g., US Caselaw Access Project CC0, France Licence Ouverte 2.0, Finland/Austria CC BY 4.0); tools emit a `Credit:` line |
| worldwidelaw/legal-sources | Open source | Publicly available government data; per-source details in each `config.yaml` |
| Ansvar-Systems | Apache-2.0 | Corpora served via the gateway with verbatim citations; self-built corpora must respect upstream licenses |

**Citation discipline**: anything obtained from these sources must be reported honestly in Part 3 ("Channels and sources") of the Ascertainment Opinion and in the Research Log — tool/repository used and retrieval date. Honor `Credit:` requirements (e.g., French DILA data) as stated.
