---
name: paper-writer
description: "Medical/scientific paper writing workflow skill. Manages the full pipeline from literature search to submission-ready manuscript. Creates and manages a project directory with IMRAD-format section files, literature matrix, reference management, and quality checklists. Supports both English and Vietnamese papers. Triggers: 'write paper', 'paper-write', 'start manuscript', '論文を書く', '論文執筆', '論文プロジェクト', 'manuscript', 'research paper', '原稿作成'."
---

# Paper Writer Skill

Full-pipeline academic paper writing assistant. From literature search to submission-ready manuscript.

## Overview

This skill manages the entire paper writing workflow:

```
Literature Search → Outline → Tables/Figures → Draft → Humanize → References → Quality Review → Pre-Submission → [Revision] → [Post-Acceptance] → [Rejection → Resubmission]
```

Each paper is a **project directory** containing structured Markdown files for every section, a literature matrix, and quality checklists.

### Supported Paper Types

| Type | Structure | Reporting Guideline | Notes |
|------|-----------|-------------------|-------|
| **Original Article** | Full IMRAD | STROBE / CONSORT | Default |
| **Case Report** | Intro / Case / Discussion | CARE | Separate templates |
| **Review Article** | Thematic sections | - | Flexible structure |
| **Letter / Short Communication** | Condensed IMRAD | Same as original | Word limit focus |
| **Systematic Review** | PRISMA-compliant | PRISMA 2020 | With PRISMA checklist |
| **Study Protocol** | SPIRIT-compliant | SPIRIT 2025 | For trial registration papers |

## Workflow

### Phase 0: Project Initialization

When the user invokes this skill, ask for:

1. **Working title** (can change later)
2. **Paper type** (Original Article / Case Report / Review / Letter / Systematic Review)
3. **Target journal** (optional but recommended)
4. **Language** (English / Vietnamese / Both)
5. **Research question** in one sentence
6. **Key data** available (what Tables/Figures already exist?)

#### Step 0.1: Capture Journal Requirements

If a target journal is specified, look up and document:
- **Word limits**: total manuscript, abstract, each section (if specified)
- **Citation style**: Vancouver, APA, NLM, or other
- **Required sections**: some journals require separate Conclusion, others don't
- **Abstract format**: structured or unstructured, word limit
- **Figure/Table limits**: maximum number allowed
- **Reporting guideline**: which checklist the journal requires
- **Special requirements**: cover page format, line numbering, etc.
- **AI disclosure**: whether the journal requires AI usage disclosure, and where (Methods, Acknowledgments, or dedicated section). See `references/ai-disclosure.md`.
- **Keywords**: number required, MeSH preferred or free-text. See `references/keywords-guide.md`.
- **Graphical abstract**: required or optional. See `templates/graphical-abstract.md`.

Use `search_web` to look up the journal's "Instructions for Authors" page.

Record all requirements in the README.md under a "Journal Requirements" section.

#### Step 0.2: Select Reporting Guideline

Based on paper type and study design, select the appropriate reporting guideline:

| Study Type | Guideline | Reference |
|-----------|-----------|-----------|
| Randomized Controlled Trial | CONSORT 2025 | `references/reporting-guidelines-full.md` |
| Observational study (cohort, case-control, cross-sectional) | STROBE | `references/reporting-guidelines-full.md` |
| Systematic review / meta-analysis | PRISMA 2020 | `references/reporting-guidelines-full.md` |
| Case report | CARE | `references/reporting-guidelines-full.md` |
| Diagnostic accuracy study | STARD 2015 | `references/reporting-guidelines-full.md` |
| Quality improvement study | SQUIRE 2.0 | `references/reporting-guidelines-full.md` |
| Study protocol (clinical trial) | SPIRIT 2025 | `references/reporting-guidelines-full.md` |
| Prediction model (incl. AI/ML) | TRIPOD+AI 2024 | `references/reporting-guidelines-full.md` |
| Animal research | ARRIVE 2.0 | `references/reporting-guidelines-full.md` |
| Health economics | CHEERS 2022 | `references/reporting-guidelines-full.md` |

Read `[workspace]/paper-writer-skill-antigravity/references/reporting-guidelines.md` (summary) or `references/reporting-guidelines-full.md` (comprehensive) and note the key checklist items for the selected guideline. These items will be checked throughout the writing process.

#### Step 0.3: Create Project Directory

**For Original Article / Review / Letter / Systematic Review:**

```
{project-dir}/
├── README.md                        # Project dashboard (status, timeline, links)
│
├── 00_literature/                   # Phase 1: Literature
│   ├── search-strategy.md           #   Search terms, databases, dates
│   ├── literature-matrix.md         #   Structured comparison table
│   └── key-papers/                  #   Notes on important papers (1 file per paper)
│
├── 01_outline.md                    # Phase 2: Paper skeleton
│
├── sections/                        # Phase 3: Manuscript sections (writing order)
│   ├── 02_methods.md
│   ├── 03_results.md
│   ├── 04_introduction.md
│   ├── 05_discussion.md
│   ├── 06_conclusion.md
│   ├── 07_abstract.md
│   └── 08_title.md
│
├── tables/                          # Tables (numbered: table1_baseline.md, ...)
├── figures/                         # Figures + captions (fig1_caption.md, ...)
├── supplements/                     # Supplementary materials
│   ├── supplementary-tables/        #   e.g., tableS1_sensitivity.md
│   ├── supplementary-figures/       #   e.g., figS1_subgroup.md
│   └── appendices/                  #   Additional methods, datasets, etc.
│
├── data/                            # Research data (see templates/data-management.md)
│   ├── raw/                         #   Original data (READ-ONLY, gitignored)
│   ├── processed/                   #   Cleaned, de-identified data
│   ├── analysis/                    #   Statistical output, scripts
│   └── data-dictionary.md           #   Variable definitions
│
├── ethics/                          # Ethics & regulatory
│   ├── irb-approval.md              #   IRB approval details, number, dates
│   ├── informed-consent.md          #   Consent process documentation
│   ├── protocol.md                  #   Study protocol (SPIRIT if applicable)
│   └── registration.md              #   Trial/study registration (UMIN, ClinicalTrials.gov)
│
├── submissions/                     # Submission history (1 subfolder per attempt)
│   └── v1_{journal}/                #   e.g., v1_bmj/
│       ├── compiled-manuscript.md   #     Full compiled manuscript snapshot
│       ├── cover-letter.md          #     Cover letter
│       ├── title-page.md            #     Title page
│       ├── declarations.md          #     Ethics, COI, funding, AI disclosure
│       ├── highlights.md            #     Key points (if required)
│       ├── graphical-abstract.md    #     Graphical abstract (if required)
│       └── submission-log.md        #     Date, portal, manuscript #, status
│
├── revisions/                       # Revision rounds (Phase 8)
│   └── r1/                          #   Round 1
│       ├── reviewer-comments.md     #     Original reviewer comments
│       ├── response-letter.md       #     Point-by-point response
│       ├── revision-cover-letter.md #     Revision cover letter
│       ├── diff-summary.md          #     Changes made (section, line, change)
│       └── compiled-manuscript.md   #     Revised manuscript snapshot
│
├── coauthor-review/                 # Co-author feedback tracking
│   ├── review-tracker.md            #   Who reviewed, when, status
│   └── feedback/                    #   Individual feedback files
│
├── correspondence/                  # Editor & reviewer communication log
│   └── YYYY-MM-DD_{subject}.md      #   e.g., 2026-03-05_decision-letter.md
│
├── references/                      # Reference management
│   └── 09_references.md             #   Formatted reference list
│
├── checklists/                      # Quality control
│   ├── section-quality.md           #   Per-section quality scores
│   ├── submission-ready.md          #   Pre-submission checklist
│   ├── reporting-guideline.md       #   CONSORT/STROBE/etc. item tracking
│   ├── gate-state.md                #   Stage-gate iteration state
│   └── feedback-*.md                #   Auto-generated gate feedback
│
└── log/                             # Decision & progress log
    ├── decisions.md                 #   Key decisions with rationale
    ├── meetings.md                  #   Meeting notes (co-authors, supervisor)
    └── timeline.md                  #   Milestone targets & actual dates
```

**For Case Report:**

```
{project-dir}/
├── README.md                        # Project dashboard
│
├── 00_literature/
│   ├── search-strategy.md
│   ├── literature-matrix.md
│   └── key-papers/
│
├── 01_outline.md
│
├── sections/
│   ├── 02_case.md                   # Case presentation (CARE structure)
│   ├── 03_introduction.md           # Introduction (why reportable)
│   ├── 04_discussion.md
│   ├── 05_abstract.md               # Abstract (CARE format)
│   └── 06_title.md                  # Title (must contain "case report")
│
├── tables/
├── figures/
├── supplements/
│   ├── supplementary-tables/
│   ├── supplementary-figures/
│   └── appendices/
│
├── data/
│   ├── raw/
│   ├── processed/
│   ├── analysis/
│   └── data-dictionary.md
│
├── ethics/
│   ├── irb-approval.md
│   ├── informed-consent.md          # Patient consent for publication
│   └── patient-perspective.md       # Patient's perspective (CARE item)
│
├── submissions/
│   └── v1_{journal}/
│       ├── compiled-manuscript.md
│       ├── cover-letter.md
│       ├── title-page.md
│       ├── declarations.md
│       └── submission-log.md
│
├── revisions/
│   └── r1/
│       ├── reviewer-comments.md
│       ├── response-letter.md
│       ├── diff-summary.md
│       └── compiled-manuscript.md
│
├── coauthor-review/
│   ├── review-tracker.md
│   └── feedback/
│
├── correspondence/
│   └── YYYY-MM-DD_{subject}.md
│
├── references/
│   └── 07_references.md
│
├── checklists/
│   ├── section-quality.md
│   ├── submission-ready.md
│   ├── reporting-guideline.md
│   ├── gate-state.md
│   └── feedback-*.md
│
└── log/
    ├── decisions.md
    ├── meetings.md
    └── timeline.md
```

Read `[workspace]/paper-writer-skill-antigravity/templates/project-init.md` with the `view_file` tool and use it to generate `README.md`. For Case Reports, use `project-init-case.md` instead.

**File numbering follows the recommended writing order**, not the reading order. This is intentional.

#### Step 0.4: Organize Research Data

If the user has existing research data (clinical records, CSV files, statistical output, etc.):

1. Create `data/raw/`, `data/processed/`, `data/analysis/` directories
2. Read `[workspace]/paper-writer-skill-antigravity/templates/data-management.md` for the full template
3. Ask the user to place raw data files in `data/raw/` — these files are **READ-ONLY** from this point
4. Create `data/raw/README.md` documenting the data source, extraction date, and IRB information
5. Create `data/data-dictionary.md` listing all variables with types, ranges, and labels
6. Confirm de-identification status — if not yet de-identified, create a processing plan in `data/processed/README.md`

**Security rules:**
- NEVER commit patient-identifiable data to git
- Add `data/raw/*.csv`, `data/raw/*.xlsx` etc. to `.gitignore` if the repository is shared
- Always confirm IRB approval number before proceeding with data analysis

**Data flow:** `raw/` (never modify) → `processed/` (clean, de-identify) → `analysis/` (statistical output) → `tables/` and `figures/` (manuscript-ready)

#### Step 0.5: Data Analysis

If the user has quantitative data ready for analysis, Antigravity can execute Python scripts directly. Read `[workspace]/paper-writer-skill-antigravity/templates/analysis-workflow.md` for the full workflow.

**Available analysis scripts:**

| Script | Purpose | Key Output |
|--------|---------|------------|
| `scripts/table1.py` | Table 1 (baseline characteristics) | Markdown table with N, %, mean±SD, P values |
| `scripts/analysis-template.py` | Statistical analyses | Descriptive stats, t-test, logistic regression, survival |
| `scripts/forest-plot.py` | Forest plot (meta-analysis) | PNG + SVG |

**Workflow:**

1. **Inspect data**: Load `data/processed/cohort_final.csv`, check shape, dtypes, missing values
2. **Table 1**: Run `scripts/table1.py` to generate baseline characteristics table → `tables/table1.md`
3. **Primary analysis**: Choose analysis type based on study design:
   - Cross-sectional / case-control → logistic regression (OR with 95% CI)
   - Cohort with time-to-event → survival analysis (Kaplan-Meier, log-rank)
   - Continuous outcome → linear regression
   - Group comparison → t-test / Mann-Whitney U
4. **Subgroup & sensitivity analyses**: By sex, age group, disease severity, etc.
5. **Generate figures**: Box plots, KM curves, forest plots, ROC curves
6. **Link to manuscript**: Map analysis output to Results section paragraphs

**Analysis output directory:** All results go to `data/analysis/`. Figures for the manuscript go to `figures/`.

**Required Python packages:** `numpy`, `pandas`, `scipy`, `statsmodels`, `lifelines`, `matplotlib`, `seaborn`

```bash
pip install numpy pandas scipy statsmodels lifelines matplotlib seaborn scikit-learn
```

**Statistical reporting requirements** (before writing Results):
- Effect sizes with 95% confidence intervals
- P values to 3 decimal places (P < 0.001 for very small)
- Statistical test names specified
- Software and version documented
- Two-sided tests (unless justified)
- Multiple comparison correction (if >1 primary outcome)
- Missing data handling described

See `references/statistical-reporting-full.md` for detailed SAMPL guidelines and `templates/analysis-workflow.md` for step-by-step commands.

### Phase 1: Literature Search & Organization

#### Step 1.1: Define Search Strategy

Create `00_literature/search-strategy.md` with:

- **Databases**: Consensus (via `mcp_Consensus_search`), PubMed, Google Scholar
- **Search terms**: Academic terminology
- **Inclusion/exclusion criteria** for papers
- **Date range**

**How to search:**

Use the `mcp_Consensus_search` tool to search over 200 million peer-reviewed academic papers.
- Use `query` to specify the research topic. Be specific and use academic terminology.
- You can filter using parameters like `year_min`, `study_types`, and `human`.
- This tool returns paper titles, authors, abstracts, citation counts, and direct URLs.

If `mcp_Consensus_search` results are limited, supplement with `search_web` or ask the user to provide key papers they already know.

**Practical reality**: AI-based literature search has significant limitations. The most reliable workflow is:
1. Ask the user to provide their 3-5 key papers (they usually know them already)
2. Use `mcp_Consensus_search` to find high-quality, peer-reviewed citations to fill in the gaps.
3. Use `references/pubmed-query-builder.md` to construct proper PubMed queries if needed.
4. Have the user validate the final literature list for completeness.

#### Step 1.2: Build Literature Matrix

Read `[workspace]/paper-writer-skill-antigravity/templates/literature-matrix.md` with the `view_file` tool.

For each relevant paper found, extract and organize:

| Author (Year) | Design | N | Population | Key Finding | Limitation | Relevance |
|----------------|--------|---|------------|-------------|------------|-----------|

Aim for **15-30 papers** for an original article, **8-15** for a case report, **30-50** for a systematic review.

#### Step 1.3: Identify Key Papers

For the 3-5 most important papers, create individual notes in `00_literature/key-papers/` with:

- Full citation
- Study design and quality assessment
- Key results with exact numbers
- How it relates to the current paper
- What gap it leaves (that our paper addresses)

### Phase 2: Outline

Create `01_outline.md` with the paper skeleton.

Read `[workspace]/paper-writer-skill-antigravity/references/imrad-guide.md` with the `view_file` tool for the detailed IMRAD structure. For Case Reports, this guide does not apply directly — use the CARE structure instead.

The outline should specify:

- Each section's key points (bullet list)
- Which papers support which points
- Which Tables/Figures go where
- The **story arc**: Background Problem → Gap → Our Approach → Findings → Implications
- For Case Reports: Background → Why Reportable → Case Details → Clinical Lesson

**Get user approval on outline before proceeding to drafting.**

### Phase 2.5: Tables & Figures

Read `[workspace]/paper-writer-skill-antigravity/references/tables-figures-guide.md` with the `view_file` tool.

Tables and figures are the backbone of a paper — many reviewers look at the abstract, then the tables/figures, before reading the text. **Design them before writing prose** so the text can reference them naturally.

#### Step 2.5.1: Plan Tables & Figures

Based on the outline, determine:
- Which data belongs in a table vs. a figure vs. the text
- Table 1 is almost always "Baseline Characteristics" (use the template in `references/tables-figures-guide.md`)
- How many tables/figures are allowed by the journal (check Phase 0 requirements)

#### Step 2.5.2: Create Tables

Create table files in `tables/` directory:
- `table1_baseline.md` — Baseline characteristics (standard format)
- `table2_*.md` — Additional tables as needed (regression results, outcomes, etc.)

**Rules:**
- Title above the table
- No vertical lines (horizontal lines only)
- Consistent decimal places within each column
- Footnotes for abbreviations and statistical tests
- Total sample size in the header row

#### Step 2.5.3: Plan Figures

Create caption files in `figures/` directory:
- `fig1_caption.md` — Often a flow diagram (CONSORT/PRISMA) or study design
- `fig2_caption.md` — Key result visualization

**Rules:**
- Captions must be self-explanatory without reading the main text
- Include key statistics in captions
- Specify resolution requirements (300+ DPI for print, 600+ for line art)
- Use colorblind-friendly palettes

#### Step 2.5.4: Graphical Abstract (if required)

If the journal requires or encourages a graphical abstract, read `[workspace]/paper-writer-skill-antigravity/templates/graphical-abstract.md` and plan the visual summary.

**Get user review on table/figure plan before proceeding to drafting.**

### Phase 3: Drafting

**The writing order is intentional and produces better papers.** Follow it strictly.

---

#### 3-A: Original Article Workflow

##### Step 3.1: Methods & Results (Write as a pair)

Read `[workspace]/paper-writer-skill-antigravity/templates/methods.md` and `[workspace]/paper-writer-skill-antigravity/templates/results.md` with the `view_file` tool.

**Methods rules:**
- Reproducibility is everything
- Include: study design, patients/subjects, data collection, statistical analysis, ethics
- Every method must have a corresponding result

**Results rules:**
- Facts only, no interpretation
- No references to other studies
- Every Table/Figure must be mentioned in text
- Methods ↔ Results must correspond 1:1

Write `sections/02_methods.md` and `sections/03_results.md` together, ensuring perfect correspondence. Cross-check: every subsection in Methods must map to a corresponding subsection in Results, and vice versa.

**Workflow**: Write Methods subsection 1 → Results subsection 1 → Methods subsection 2 → Results subsection 2 → ... This interleaving ensures 1:1 correspondence.

##### Step 3.2: Introduction (Paragraph 3) & Conclusion (Write as a pair)

Read `[workspace]/paper-writer-skill-antigravity/templates/introduction.md` and `[workspace]/paper-writer-skill-antigravity/templates/conclusion.md` with the `view_file` tool.

**Why write Paragraph 3 first?** The study objective (Introduction P3) and the conclusion must mirror each other. Writing them together guarantees alignment. Paragraphs 1-2 provide background that funnels toward the objective — they are easier to write once the objective is locked.

**Introduction structure (3 paragraphs):**
1. General background (everyone agrees with this)
2. Clinical question / knowledge gap (but we don't know X)
3. Study objective (therefore, we investigated...)

**Conclusion rules:**
- Must directly answer the objective stated in Introduction paragraph 3
- One core message
- Brief and direct

Write the final paragraph of `sections/04_introduction.md` and `sections/06_conclusion.md` together to ensure they mirror each other.

##### Step 3.3: Discussion

Read `[workspace]/paper-writer-skill-antigravity/templates/discussion.md` with the `view_file` tool.

**Discussion structure:**
1. Summary of main findings
2-N. Comparison with prior literature (use `00_literature/literature-matrix.md`)
N+1. Limitations — read `[workspace]/paper-writer-skill-antigravity/templates/limitations-guide.md` for categories, templates, and bilingual examples
N+2. Clinical implications / future directions

**Discussion rules:**
- No new results
- No excessive speculation
- Support every claim with a reference
- Keep it focused
- Limitations subsection is mandatory — be specific about direction of bias and mitigation

##### Step 3.4: Introduction (Paragraphs 1-2)

Now write paragraphs 1-2 of `sections/04_introduction.md`. The background should funnel toward the research question already written in paragraph 3.

##### Step 3.5: Abstract

Read `[workspace]/paper-writer-skill-antigravity/templates/abstract.md` with the `view_file` tool.

Write `sections/07_abstract.md` as a structured abstract:
- Background/Objective (1-2 sentences)
- Methods (2-3 sentences)
- Results (3-4 sentences)
- Conclusions (1-2 sentences)

Check the journal-specific word limit captured in Phase 0. The Abstract must be consistent with the full text. Cross-check all numbers.

##### Step 3.6: Title

Write `sections/08_title.md` with 3-5 title candidates. Evaluate each against:
- Specific (what was studied?)
- Concise (< 15 words ideal)
- Contains keywords (searchable)
- No conclusion spoilers

**Get user approval on final title.**

---

#### 3-B: Case Report Workflow

##### Step 3.1-CR: Case Presentation

Read `[workspace]/paper-writer-skill-antigravity/templates/case-report.md` with the `view_file` tool.

Write `02_case.md` following the CARE structure:
1. Patient information (demographics, history)
2. Clinical findings
3. Timeline (consider a timeline figure)
4. Diagnostic assessment
5. Therapeutic intervention
6. Follow-up and outcomes
7. Patient perspective (CARE item 10) — when possible, include the patient's own experience in their words

**Rules:**
- Chronological order
- Only clinically relevant details
- Document informed consent for publication
- Report both positive AND negative findings
- Patient perspective strengthens the report and is recommended by CARE guidelines

##### Step 3.2-CR: Discussion

Read `[workspace]/paper-writer-skill-antigravity/templates/discussion.md` with the `view_file` tool.

Write `04_discussion.md`:
1. Why this case is significant (clinical lesson)
2. Comparison with published literature
3. Limitations of the case
4. Clinical implications

Keep it focused and shorter than in an Original Article.

##### Step 3.3-CR: Introduction

Read `[workspace]/paper-writer-skill-antigravity/templates/case-introduction.md` with the `view_file` tool.

Write `03_introduction.md`:
1. Brief background on the condition
2. Why this case is reportable (rarity, novelty, instructive value)
3. Optional: "We report a case of... to highlight..."

Write the Introduction AFTER the Case section — you need to know the full case to justify its reporting.

##### Step 3.4-CR: Abstract

Read `[workspace]/paper-writer-skill-antigravity/templates/case-abstract.md` with the `view_file` tool.

Write `05_abstract.md` using the CARE abstract structure:
- Background (1-2 sentences: why this case is worth reporting)
- Case Presentation (3-5 sentences: demographics, findings, diagnosis, treatment, outcome)
- Conclusions (1-2 sentences: clinical lesson)

Do NOT use Methods/Results structure for Case Report abstracts.

##### Step 3.5-CR: Title

Write `06_title.md` with 3-5 title candidates. For case reports:
- Title MUST contain "case report" (CARE requirement)
- Include the diagnosis or key finding
- Example: "Successful treatment of severe pediatric asthma with dupilumab: a case report"

**Get user approval on final title.**

---

#### 3-C: Review Article Workflow

Review articles synthesize existing literature on a topic. The structure is thematic rather than IMRAD.

##### Step 3.1-RA: Thematic Sections

Read `[workspace]/paper-writer-skill-antigravity/templates/discussion.md` for general writing guidance.

Organize the body into thematic sections based on the outline. Common structures:
1. **Chronological**: Evolution of understanding over time
2. **Thematic**: Grouped by subtopic (most common)
3. **Methodological**: Grouped by study approach

Each section should:
- Synthesize findings across studies (not just summarize one at a time)
- Identify areas of consensus and controversy
- Highlight gaps in the literature
- Use the literature matrix to ensure comprehensive coverage

##### Step 3.2-RA: Introduction

Write the introduction:
1. Scope and importance of the topic
2. Why a review is needed now (new evidence, controversy, emerging field)
3. Objectives and scope of this review

##### Step 3.3-RA: Conclusion & Future Directions

Write the conclusion:
1. Synthesize the key themes identified
2. Current state of knowledge
3. Gaps and future research directions
4. Clinical implications (if applicable)

##### Step 3.4-RA: Abstract

Write an unstructured abstract (unless journal requires structured format):
- Purpose of the review
- Methods (databases searched, date range, selection criteria)
- Key findings synthesized across themes
- Conclusions

##### Step 3.5-RA: Title

Write title candidates. For review articles:
- Include "review", "narrative review", or "scoping review" in the title
- Clearly state the topic
- Example: "Artificial intelligence in diagnostic radiology: a narrative review"

**Get user approval on final title.**

---

#### 3-D: Systematic Review Workflow

Read `[workspace]/paper-writer-skill-antigravity/templates/sr-outline.md` with the `view_file` tool for the complete PRISMA 2020-compliant template.

Systematic reviews follow a strict, pre-registered protocol. The template provides the full structure with PRISMA 2020 checklist item numbers.

##### Step 3.1-SR: Methods

The Methods section is the most critical part. Write it following PRISMA items P-5 through P-18:
1. Protocol and registration (PROSPERO ID)
2. Eligibility criteria (PICO/PECO)
3. Information sources (databases, dates)
4. Search strategy (full strategy in supplementary)
5. Selection process (screening, inter-rater reliability)
6. Data collection process
7. Data items
8. Risk of bias assessment (tool selection)
9. Effect measures
10. Synthesis methods (narrative and/or meta-analysis)
11. Subgroup and sensitivity analyses
12. Reporting bias assessment
13. Certainty of evidence (GRADE)

##### Step 3.2-SR: Results

Write Results following PRISMA items P-19 through P-23:
1. PRISMA flow diagram (Figure 1 — mandatory)
2. Study characteristics table
3. Risk of bias summary
4. Results of individual studies
5. Results of syntheses (forest plots if meta-analysis)
6. Reporting biases (funnel plots if ≥10 studies)
7. Certainty of evidence (GRADE Summary of Findings table)

##### Step 3.3-SR: Discussion

Write Discussion following PRISMA items P-25 through P-27:
1. Summary of evidence with certainty levels
2. Comparison with previous reviews
3. Strengths and limitations (both evidence and review process)
4. Implications for practice and research

##### Step 3.4-SR: Introduction, Abstract, Title

Follow the same principles as Original Article but with SR-specific framing:
- Introduction: justify why this SR is needed (no existing SR, outdated SR, new evidence)
- Abstract: must include number of studies, total participants, key pooled estimates
- Title: must include "systematic review" (and "meta-analysis" if applicable)

**Get user approval on final title.**

---

#### 3-E: Letter / Short Communication Workflow

Letters and short communications follow a condensed IMRAD format. The key constraint is the **word limit** (typically 600-1500 words).

##### Step 3.1-LT: Condensed Draft

Write a single file covering all sections:
1. **Introduction** (1-2 sentences): State the purpose directly. No lengthy background.
2. **Methods** (1 paragraph): Essential details only. Reference a fuller description elsewhere if needed.
3. **Results** (1-2 paragraphs): Key findings only. Usually 1 table OR 1 figure (not both).
4. **Discussion** (1-2 paragraphs): Main interpretation, 1-2 comparisons with literature, key limitation.

**Rules:**
- Every word counts — eliminate all filler
- Typically limited to 1 table + 1 figure, or 2 of one type
- References usually limited to 10-15
- No separate Conclusion section (fold into last Discussion paragraph)

##### Step 3.2-LT: Abstract

Write a brief abstract (often 100-150 words, unstructured).

##### Step 3.3-LT: Title

Short, direct titles work best. No need for elaborate structure.

**Get user approval on final title.**

### Phase 4: Humanize

Read `[workspace]/paper-writer-skill-antigravity/references/humanizer-academic.md` with the `view_file` tool.

After drafting, run a humanization pass on every section to remove AI-generated writing patterns.

#### Step 4.1: Scan for AI Patterns

Read each section file and identify:

**English papers** — check for these 18 patterns:
1. Significance inflation ("pivotal", "evolving landscape", "underscores")
2. Notability claims ("landmark", "renowned", "groundbreaking")
3. Superficial -ing analyses ("highlighting", "underscoring", "showcasing")
4. Promotional language ("profound impact", "remarkable", "dramatic")
5. Vague attributions ("Studies have shown", "Experts argue")
6. Formulaic challenges ("Despite challenges... future outlook")
7. AI vocabulary ("Additionally", "crucial", "delve", "landscape", "pivotal")
8. Copula avoidance ("serves as" instead of "is")
9. Negative parallelisms ("Not only... but also")
10. Rule of three overuse (forcing ideas into groups of three)
11. Synonym cycling ("Patients... Participants... Subjects")
12. False ranges ("from X to Y" on unrelated scales)
13. Em dash overuse
14. Title Case in headings
15. Curly quotation marks
16. Filler phrases ("In order to", "It is important to note", "comprehensive investigation")
17. Excessive hedging ("may suggest... have the potential to")
18. Generic positive conclusions ("The future looks bright")

**Vietnamese papers (Tiếng Việt)** — Check 13 patterns (A-C) + AI Vocabulary list (D):

A. Punctuation and Formatting (3 patterns):
- Overuse of em-dashes, quotation marks, and excessive parenthetical notes

B. Sentence Rhythm (3 patterns):
- Repetitive sentence endings
- Overuse of transitional words (Furthermore, Moreover, In addition)
- Every paragraph wraps up too neatly

C. Academic Writing Issues (7 patterns):
- C-1 Excessive hedging
- C-2 Unsubstantiated evaluative words (highly effective, huge benefit)
- C-3 Relying entirely on abstract words
- C-4 AI vocabulary (comprehensive, innovative, seamless, thought-provoking)
- C-5 Relentless synonym cycling
- C-6 Excessive use of passive voice
- C-7 Inclusion of non-academic tone ("Hope this helps", "The key points are as follows" → delete)

D. AI Vocabulary List: Refer to the Tiếng Việt section D in `references/humanizer-academic.md`. Use this list to check for pattern C-4.

#### Step 4.2: Rewrite

Consult `references/humanizer-academic.md` for specific before/after examples. For each identified pattern:
1. Replace with precise, specific academic language
2. Preserve all data, statistics, and citations exactly
3. Use simple constructions ("is" over "serves as")
4. Remove filler and reduce hedging to match evidence strength
5. Ensure consistent terminology throughout
6. If 3+ AI patterns appear in one sentence, rewrite the entire sentence rather than fixing patterns individually

#### Step 4.3: Section-Specific Focus

**English:**

| Section | Priority Patterns |
|---------|------------------|
| Introduction | #1 Significance inflation, #5 Vague attributions, #7 AI vocabulary, #3 -ing analyses |
| Methods | #16 Filler phrases, #8 Copula avoidance |
| Results | #3 -ing analyses, #4 Promotional language |
| Discussion | #17 Excessive hedging, #6 Formulaic challenges |
| Conclusion | #18 Generic conclusions, #1 Significance inflation |
| Abstract | ALL patterns (most visible section) |

**Tiếng Việt:**

| セクション | 重点パターン |
|-----------|-------------|
| 緒言 | C-2 根拠なき評価語, B-2 接続詞過多 |
| 方法 | C-6 受動態の過剰使用, C-3 抽象語 |
| 結果 | B-1 同じ語尾, A-3 丸括弧多用 |
| 考察 | C-1 保険が多い, C-4 AIボキャブラリー |
| 結論 | C-2 根拠なき評価語, C-7 非学術的文体 |
| 抄録 | 全パターン |

#### Step 4.4: Verify

After humanization:

**English:**
- [ ] Scientific content unchanged (no data or citations lost)
- [ ] No "Additionally" / "Furthermore" at sentence start (max 1 per section)
- [ ] No "pivotal" / "crucial" / "landscape" / "delve"
- [ ] No "-ing" phrases tacked on for fake depth
- [ ] No "serves as" / "stands as" (use "is")
- [ ] Em dashes used sparingly (< 2 per page)
- [ ] Consistent terminology (no synonym cycling)
- [ ] Sentence rhythm varies (short and long sentences mixed)
- [ ] No generic conclusions remaining
- [ ] Hedging proportionate to evidence strength

**Tiếng Việt:**
- [ ] No repetitive use of transitional words (max 1 per section)
- [ ] No repetitive sentence endings (max 3 times in a row)
- [ ] No unsubstantiated evaluative words ("vô cùng", "to lớn")
- [ ] No excessive passive voice (change to active)
- [ ] No generic closing remarks
- [ ] No over-reliance on abstract words
- [ ] No overuse of quotation marks

### Phase 5: References

Read `[workspace]/paper-writer-skill-antigravity/references/citation-guide.md` with the `view_file` tool.

Build `references/09_references.md` (or `references/07_references.md` for Case Reports):

1. Collect all cited papers from all sections
2. Format according to target journal style captured in Phase 0 (Vancouver, APA, etc.)
3. Number sequentially as cited
4. Verify completeness: every reference is cited in text, every citation has a reference entry
5. **Verify authenticity**: For EVERY AI-suggested reference, confirm the paper exists via `search_web` with the exact title. AI frequently fabricates plausible-sounding citations.

### Phase 6: Quality Review

Read `[workspace]/paper-writer-skill-antigravity/references/section-checklist.md` with the `view_file` tool. For Case Reports, also check the CARE-specific items in `templates/case-report.md`.

Run the quality checklist against each section. Update `checklists/section-quality.md` with results.

**Verification checklist:**
- [ ] Methods ↔ Results correspondence (Original Article only)
- [ ] Introduction objective ↔ Conclusion answer
- [ ] All Tables/Figures mentioned in text
- [ ] No interpretation in Results (Original Article only)
- [ ] No new results in Discussion
- [ ] Abstract numbers match full text
- [ ] All references cited and formatted
- [ ] Word count within target journal limits (check Phase 0 requirements)
- [ ] Reporting guideline followed (check Phase 0 selected guideline)
- [ ] AI writing patterns removed (Phase 4 verification passed)
- [ ] Consistent terminology throughout all sections
- [ ] Ethics approval and informed consent documented

### Phase 7: Pre-Submission

Read `[workspace]/paper-writer-skill-antigravity/templates/cover-letter.md` and `[workspace]/paper-writer-skill-antigravity/templates/submission-ready.md` with the `view_file` tool.

Create:
1. **Title page** — read `[workspace]/paper-writer-skill-antigravity/templates/title-page.md` for the template (running head, all authors with ORCID, affiliations, word counts, corresponding author, clinical trial registration)
2. **Highlights / Key Points** — read `[workspace]/paper-writer-skill-antigravity/templates/highlights.md` and create the appropriate summary box for the target journal (VIMA Key Points, BMJ "What is known", Elsevier Highlights, Lay Summary, etc.)
3. **Acknowledgments** — read `[workspace]/paper-writer-skill-antigravity/templates/acknowledgments.md` and draft (non-author contributions, AI tool disclosure, patient acknowledgment)
4. **Declarations** — read `[workspace]/paper-writer-skill-antigravity/templates/declarations.md` and complete (Ethics, COI using `references/coi-detailed.md`, Funding, Data Availability, AI Disclosure, CRediT)
5. Cover letter using the template
6. `checklists/submission-ready.md` using the template — fill in journal-specific limits from Phase 0
7. Compile all sections into a single reading-order Markdown file → `submissions/v1_{journal}/compiled-manuscript.md`
8. Create `submissions/v1_{journal}/submission-log.md` with submission date, portal, manuscript ID
9. Log the submission in `log/timeline.md`

**Final compilation order (reading order):**

For Original Article:
```
Title → Abstract → Introduction → Methods → Results → Discussion → Conclusion → References
```

For Case Report:
```
Title → Abstract → Introduction → Case Presentation → Discussion → References
```

The compiled file should include all section content in sequence. Tables and Figures should be referenced but kept in their separate folders. All submission documents go into `submissions/v1_{journal}/`.

### Phase 8: Revision (Post-Review)

When the user receives reviewer comments (peer review, editorial decision letter):

#### Step 8.1: Organize Reviewer Comments

Create `revisions/r1/reviewer-comments.md`:

1. Parse the decision letter and reviewer comments
2. Number each comment sequentially (R1-1, R1-2, R2-1, R2-2, etc.)
3. Categorize each comment:
   - **Must fix**: Factual errors, missing data, methodological concerns
   - **Should fix**: Reasonable suggestions that improve the paper
   - **Consider**: Optional suggestions, stylistic preferences
   - **Rebut**: Comments based on misunderstanding (requires polite explanation)

#### Step 8.2: Create Response Letter

Create `revisions/r1/response-letter.md`:

For each comment, use this format:

```
**Comment R1-1:** [Quote the reviewer's comment]

**Response:** [Your response]

**Changes made:** [Specific changes with page/line numbers, or explanation if no change]
```

**Rules for response letters:**
- Thank the reviewer for constructive feedback (once at the beginning, not per comment)
- Be specific about what was changed and where
- For rebuttals, acknowledge the reviewer's perspective, then explain with evidence
- Never be defensive or dismissive
- If a change was not made, explain why with references or data

#### Step 8.3: Implement Revisions

1. Track which sections need modification based on reviewer comments
2. Make changes in the relevant section files
3. Mark changed text (many journals require highlighted changes or a diff)
4. Roll back affected phases: re-run Humanize (Phase 4) and Quality Review (Phase 6) on modified sections
5. Update word counts and verify journal limits are still met

#### Step 8.4: Verify Revision Completeness

- [ ] Every reviewer comment has a response
- [ ] Every "Must fix" and "Should fix" item has been addressed
- [ ] Rebuttals are supported by evidence
- [ ] Changed text is marked/highlighted
- [ ] References updated if new citations added
- [ ] Abstract updated if results or conclusions changed
- [ ] Cover letter for resubmission drafted

### Phase 9: Post-Acceptance

Read `[workspace]/paper-writer-skill-antigravity/templates/proof-correction.md` with the `view_file` tool.

After acceptance, the corresponding author receives galley proofs. This is the LAST opportunity to correct errors.

#### Step 9.1: Proof Review

When proofs arrive (typically 2-8 weeks after acceptance, turnaround: 24-72 hours):

**Critical checks:**
- [ ] Author names, affiliations, and ORCID — correct?
- [ ] Abstract numbers match main text?
- [ ] All tables — data values correct, no transposition errors?
- [ ] All figures — correct images, acceptable quality?
- [ ] Reference list — complete, correct numbering?
- [ ] Corresponding author email — correct?
- [ ] Funding and COI statements — accurate?
- [ ] Clinical trial registration number — present?

**NOT allowed at proof stage:**
- Rewriting sentences or paragraphs
- Adding new data, references, or authors
- Changing conclusions

#### Step 9.2: Submit Corrections

Use the journal's proofing system (Proof Central, CATS, eProofing, or direct PDF return). For each correction: state page, column, line, and exact change.

#### Step 9.3: Post-Publication

After publication:
- Verify the final published version matches the accepted manuscript
- Share via institutional repository (Green OA) if applicable — see `references/open-access-guide.md`
- Update clinical trial registry with results (if applicable) — see `references/clinical-trial-registration.md`
- Share with co-authors and collaborators

### Phase 10: Rejection & Resubmission

Read `[workspace]/paper-writer-skill-antigravity/references/desk-rejection-prevention.md` and `references/journal-reformatting.md` with the `view_file` tool.

#### Step 10.1: Assess the Rejection

| Decision | Action |
|----------|--------|
| **Desk rejection (scope)** | Reformat and submit to next journal immediately |
| **Desk rejection (quality)** | Revise manuscript, then reformat and submit |
| **Peer review rejection** | Read reviews carefully; major revision before next journal |
| **Reject with encouragement to resubmit** | Treat as major revision; address all comments |

#### Step 10.2: Quick Reformat

Use `references/journal-reformatting.md` checklist:
1. Change reference format (use reference manager)
2. Restructure abstract with new headings — see `references/abstract-formats.md`
3. Adjust word count — see `references/word-count-limits.md`
4. Add/remove special sections (Key Points, Highlights)
5. Reformat title page
6. Write new cover letter (address new editor by name)
7. Verify no mention of previous journal name in manuscript

#### Step 10.3: Cascading Submission Strategy

Track submissions:

| Journal | Submitted | Decision | Turnaround | Next Action |
|---------|-----------|----------|-----------|-------------|
| [Journal 1] | YYYY-MM-DD | — | — | — |

Plan cascade: Reach journal → Target journal → Safety journal → Backup journal.

## Section-Specific AI Guidelines

### What AI Should Do

| Section | AI Role |
|---------|---------|
| Literature search | Search, organize, summarize — user validates relevance |
| Methods | Draft based on user's data description — user verifies accuracy |
| Results | Structure and format — user provides the actual data |
| Case (Case Report) | Structure chronologically — user provides clinical details |
| Introduction | Draft background from literature — user refines narrative |
| Discussion | Suggest comparisons with literature — user controls interpretation |
| Abstract | Generate from full text — user ensures accuracy |
| References | Format and organize — user verifies completeness and authenticity |

### What AI Should NOT Do

- Fabricate data or statistics
- Invent citations (always verify with `search_web`)
- Write Results without user-provided data
- Write Case Presentation without user-provided clinical details
- Make clinical recommendations beyond the data
- Skip the user approval step at outline and title phases

## Status Tracking

Update `README.md` status after each phase. Use these status values:
- **Not Started**: Phase not begun
- **In Progress**: Phase actively being worked on (add details in Notes)
- **Draft Complete**: First draft finished, pending review
- **Done**: Phase completed and reviewed

Use the appropriate status tracker based on paper type:

**Original Article:**

| Phase | Status | Last Updated |
|-------|--------|-------------|
| Literature Search | Not Started | - |
| Outline | Not Started | - |
| Tables & Figures | Not Started | - |
| Methods & Results | Not Started | - |
| Introduction & Conclusion | Not Started | - |
| Discussion | Not Started | - |
| Abstract | Not Started | - |
| Title & Keywords | Not Started | - |
| Humanize | Not Started | - |
| References | Not Started | - |
| Declarations | Not Started | - |
| Quality Review | Not Started | - |
| Pre-Submission | Not Started | - |

**Case Report:**

| Phase | Status | Last Updated |
|-------|--------|-------------|
| Literature Search | Not Started | - |
| Outline | Not Started | - |
| Tables & Figures | Not Started | - |
| Case Presentation | Not Started | - |
| Discussion | Not Started | - |
| Introduction | Not Started | - |
| Abstract | Not Started | - |
| Title & Keywords | Not Started | - |
| Humanize | Not Started | - |
| References | Not Started | - |
| Declarations | Not Started | - |
| Quality Review | Not Started | - |
| Pre-Submission | Not Started | - |

**Review Article:**

| Phase | Status | Last Updated |
|-------|--------|-------------|
| Literature Search | Not Started | - |
| Outline | Not Started | - |
| Tables & Figures | Not Started | - |
| Thematic Sections | Not Started | - |
| Introduction | Not Started | - |
| Conclusion & Future Directions | Not Started | - |
| Abstract | Not Started | - |
| Title & Keywords | Not Started | - |
| Humanize | Not Started | - |
| References | Not Started | - |
| Declarations | Not Started | - |
| Quality Review | Not Started | - |
| Pre-Submission | Not Started | - |

**Systematic Review:**

| Phase | Status | Last Updated |
|-------|--------|-------------|
| Literature Search | Not Started | - |
| Outline | Not Started | - |
| Tables & Figures | Not Started | - |
| Methods (PRISMA) | Not Started | - |
| Results (PRISMA) | Not Started | - |
| Discussion | Not Started | - |
| Introduction | Not Started | - |
| Abstract | Not Started | - |
| Title & Keywords | Not Started | - |
| Humanize | Not Started | - |
| References | Not Started | - |
| Declarations | Not Started | - |
| Quality Review | Not Started | - |
| Pre-Submission | Not Started | - |

**Letter / Short Communication:**

| Phase | Status | Last Updated |
|-------|--------|-------------|
| Literature Search | Not Started | - |
| Outline | Not Started | - |
| Tables & Figures | Not Started | - |
| Condensed Draft | Not Started | - |
| Abstract | Not Started | - |
| Title & Keywords | Not Started | - |
| Humanize | Not Started | - |
| References | Not Started | - |
| Quality Review | Not Started | - |
| Pre-Submission | Not Started | - |

## Resuming a Project

When the user invokes this skill on an existing project directory:

1. **Read `README.md`** to understand current status, paper type, target journal, and research question
2. **Scan section files** to assess actual content state:
   - Read each section file that shows "In Progress" or "Draft Complete"
   - Check word count and completeness (empty sections, TODO markers, partial drafts)
   - Compare actual file state with the status tracker — the files are the source of truth
3. **Present a summary to the user**: "Here is where we left off: [status]. The next step is [phase]. Shall I continue?"
4. **Check for workflow updates**: Compare the README status table against the canonical phase list above. If phases are missing (e.g., old project created before "Humanize" was added), add them with "Not Started" status and inform the user
5. **Resume from the next incomplete phase**
6. **Update status tracker**

### Handling Mid-Project Changes

**Changing target journal**: If the user wants to change the target journal:
1. Update README.md Paper Info and Journal Requirements
2. Re-check: citation style, word limits, abstract format, reporting guideline
3. Reformat references if citation style changed
4. Check word counts against new limits
5. Update cover letter

**Adding data or revisions**: If the user has new data or reviewer feedback:
1. Identify which sections are affected
2. Roll back affected phases to "In Progress"
3. Re-run from that phase forward (including Humanize and Quality Review)

## Language Support

### English Papers
- Use standard academic English
- Follow target journal's style guide
- Flag awkward phrasing for user review

### Vietnamese Papers
- IMRAD format is identical to English papers (Case Reports follow CARE format)
- Use formal academic tone
- Technical terms should be in Vietnamese by default (with English equivalent in parentheses on first use)
- For Case Reports, use standard headings like "Trình bày ca lâm sàng", "Diễn tiến lâm sàng"
- Refer to any separate paper writing guides if provided

## Team Mode

When the user specifies "team mode", "parallel", or similar, run the phases with parallel agents to significantly speed up the process.

### Team Composition

| エージェント | 役割 | エージェント定義 | モデル |
|------------|------|----------------|--------|
| 文献検索 | DB別の並列論文検索 | `[workspace]/paper-writer-skill-antigravity/agents/paper-lit-searcher.md` | Gemini 3.1 Pro |
| 表・図設計 | 表と図の並列設計 | `[workspace]/paper-writer-skill-antigravity/agents/paper-table-figure-planner.md` | Gemini 3.1 Pro |
| セクション執筆 | 汎用セクション執筆 | `[workspace]/paper-writer-skill-antigravity/agents/paper-section-drafter.md` | Gemini 3.1 Pro |
| ヒューマナイザー | AI文体パターン除去 | `[workspace]/paper-writer-skill-antigravity/agents/paper-humanizer.md` | Gemini 3.1 Flash |
| 参考文献 | 引用収集・検証 | `[workspace]/paper-writer-skill-antigravity/agents/paper-ref-builder.md` | Gemini 3.1 Pro |
| セクションレビュー | セクション品質チェック | `[workspace]/paper-writer-skill-antigravity/agents/paper-section-reviewer.md` | Gemini 3.1 Pro |
| 品質ゲート | 横断整合性の最終検証 | `[workspace]/paper-writer-skill-antigravity/agents/paper-quality-gate.md` | Gemini 3.1 Pro (High) |

### Phase別チームワークフロー

#### Phase 0, 2: 逐次実行（変更なし）
ユーザーとの対話が必要なため、既存フローのまま実行する。

#### Phase 1: 文献検索（並列 x3）

`paper-lit-searcher` を3つ**並列**でAgent toolから起動する：

- Agent A: PubMed検索（MeSH用語使用）
- Agent B: Google Scholar検索（フリーテキスト）
- Agent C: ユーザー提供の重要論文レビュー + ドメイン固有DB（CiNii, EMBASE等）

3エージェント完了後、リードが結果をマージし `00_literature/literature-matrix.md` を作成（重複除去）。

#### Phase 2.5: 表・図（並列 x2）

`paper-table-figure-planner` を2つ**並列**で起動：

- Agent A: 表の設計（`tables/` に出力）
- Agent B: 図の設計（`figures/` に出力）

#### Phase 3: ドラフティング（グループ並列）

`paper-section-drafter` を依存関係に基づいてラウンド実行する。

**Original Article の場合:**
- **Round 1**: Methods + Results（ペアリング執筆、1エージェント）
- **Round 2**: Introduction P3 + Conclusion（並列 x2、ミラー関係）
- **Round 3**: Discussion + Introduction P1-P2 + Abstract（並列 x3）
- **Round 4**: Title（1エージェント）

**Case Report の場合:**
- **Round 1**: Case Presentation（逐次、ユーザーの臨床情報必要）
- **Round 2**: Discussion + Introduction（並列 x2）
- **Round 3**: Abstract + Title（並列 x2）

**Systematic Review の場合:**
- **Round 1**: Methods（逐次、最重要セクション）
- **Round 2**: Results（逐次、Methods構造に依存）
- **Round 3**: Discussion + Introduction + Abstract（並列 x3）
- **Round 4**: Title（1エージェント）

#### Phase 4: ヒューマナイズ（並列 x最大6）

`paper-humanizer` をセクション数分**並列**で起動：

- 各エージェントが1セクションを担当
- 全エージェントが `references/humanizer-academic.md` を参照
- 完了後、リードがPhase 4.4検証チェックリストを実行

#### Phase 5: 参考文献（2段階）

`paper-ref-builder` を2段階で実行：

1. **Builder モード**: 全セクションから引用収集→ジャーナル形式でフォーマット
2. **Verifier モード**: search_webで各文献の実在確認→捏造フラグ

#### Phase 6: 品質レビュー（並列 + ゲート）

**Round 1**: `paper-section-reviewer` をセクション数分**並列**で起動
- 各エージェントが `references/section-checklist.md` に基づき評価

**Round 2**: `paper-quality-gate` を1つ起動（opusモデル）
- 全セクションの横断整合性を検証
- PASS必須。FAILなら該当セクションを修正し再レビュー

#### Phase 7: 投稿準備（並列 x4）

`paper-section-drafter` を4つ**並列**で起動：

- Agent A: タイトルページ（`templates/title-page.md` 参照）
- Agent B: ハイライト / Key Points（`templates/highlights.md` 参照）
- Agent C: 謝辞・宣言（`templates/acknowledgments.md` + `templates/declarations.md` 参照）
- Agent D: カバーレター（`templates/cover-letter.md` 参照）

完了後、`scripts/compile-manuscript.sh` で最終統合。

#### Phase 8: リビジョン（並列 x3）

レビュアーコメントのパース・カテゴリ分けは逐次（ユーザー対話）。その後：

- Agent A (`paper-section-drafter`): Must Fix コメント対応
- Agent B (`paper-section-drafter`): Should Fix コメント対応
- Agent C (`paper-section-drafter`): 反論（Rebut）ドラフト作成

完了後、修正セクションに Phase 4（ヒューマナイズ）と Phase 6（品質レビュー）を再実行。

#### Phase 9-10: 逐次実行（変更なし）
イベント駆動（プルーフ到着、リジェクション通知）のため既存フローのまま。

### チームモードの使い分け

| 場面 | 推奨モード |
|------|-----------|
| Original Article（多セクション） | チームモード |
| Systematic Review（大量文献） | チームモード |
| Case Report（少セクション） | 逐次モード |
| Letter / Short Communication | 逐次モード |
| 締め切りが迫っている場合 | チームモード |

### Autonomous Stage-Gate System（自律品質ゲート）

チームモード時、各Phaseに品質ゲートを設ける。ゲートがFAILの場合、修正エージェントを自動再起動してPASSまでループする。最大3イテレーションでユーザーにエスカレーション。

#### ゲートフロー

```
Phase N 完了 → [ゲートエージェント] → PASS? → 次のPhaseへ
                                    → FAIL + iter<3 → FEEDBACK.md生成 → [修正エージェント(revision_mode)] → ゲートに戻る
                                    → FAIL + iter≥3 → ユーザーにエスカレーション（checklists/escalation-log.md）
```

#### Phase別ゲート定義

| Phase | ゲート名 | PASS条件 | ゲート担当 | 修正担当 |
|-------|---------|---------|-----------|---------|
| 1 | 文献品質 | ≥10論文、全DOI/URLあり、捏造なし | paper-section-reviewer | paper-lit-searcher |
| 2 | アウトライン | 全IMRAD存在、≥2引用マッピング | paper-section-reviewer | ユーザーに即エスカレ |
| 2.5 | 表・図 | 全設計ファイル完備、ジャーナル制限内 | paper-section-reviewer | paper-table-figure-planner |
| 3 | セクション | score≥80%、Must Fix=0 | paper-section-reviewer | paper-section-drafter |
| 4 | ヒューマナイズ | 高優先AIパターン残存0 | paper-section-reviewer | paper-humanizer |
| 5 | 参考文献 | 捏造0、孤立引用0 | paper-ref-builder(verifier) | paper-ref-builder(builder) |
| 6 | 横断整合 | PASS or CONDITIONAL_PASS | paper-quality-gate(Gemini 3.1 Pro (High)) | paper-section-drafter |
| 7 | 投稿準備 | 全必須書類あり、語数制限内 | paper-section-reviewer | paper-section-drafter |

#### フィードバックファイル形式

ゲートFAIL時、オーケストレーターが `checklists/feedback-{phase}-{section}.md` を生成する：

```yaml
---
revision_mode: true
iteration: {N} of 3
section: {section_name}
source_file: {path/to/section_file.md}
gate_verdict: FAIL
---
```

```markdown
## Must Fix
### Issue 1
- item: {チェックリスト項目名}
- location: {段落番号 or 行範囲}
- problem: {問題の1文記述}
- fix: {具体的な修正指示}

## Should Fix
### Issue 2
- item: {項目名}
- fix: {修正指示}

## Context (変更不可)
- reporting_guideline: {PRISMA等}
- journal: {ジャーナル名}
- language: {English/Vietnamese}
```

#### 修正エージェントの起動方法

ゲートFAIL時、修正エージェントに以下を渡す：

```
revision_mode: true
feedback_file: {project_dir}/checklists/feedback-{phase}-{section}.md
source_file: {project_dir}/{section_file.md}
```

全修正エージェント（paper-section-drafter, paper-humanizer, paper-lit-searcher, paper-table-figure-planner）は `revision_mode: true` を受け取ると、フィードバックの Must Fix 項目のみを処理し、通常の初期ワークフローをスキップする。

#### ゲート状態の永続化

`checklists/gate-state.md` でイテレーション回数を管理：

```markdown
| Phase | Section | Iteration | Status | Last Run |
|-------|---------|-----------|--------|----------|
| phase3 | methods | 2 | IN_PROGRESS | 2026-03-05 |
| phase4 | intro | 0 | PASS | 2026-03-05 |
```

#### エスカレーションプロトコル

3イテレーション到達時：
1. `checklists/escalation-log.md` に未解決の Must Fix 一覧と説明を記録
2. ユーザーにメッセージ表示（該当ファイルパスと問題点を明示）
3. ワークフローを一時停止
4. ユーザーが手動修正後「continue」で再開 → イテレーションカウンターを0にリセット

#### YAML verdict によるループ判定

section-reviewer と quality-gate は出力ファイル冒頭にYAMLヘッダを付与する：

```yaml
# section-reviewer
---
gate_verdict: PASS | FAIL
must_fix_count: {N}
score_percent: {N}
section: {name}
---

# quality-gate
---
gate_verdict: PASS | CONDITIONAL_PASS | FAIL
must_fix_count: {N}
affected_sections: [methods, results]
---
```

オーケストレーターはYAMLヘッダのみ読み取ってループ継続/終了を判定する。CONDITIONAL_PASS（Should Fixのみ残存）はPASS扱い。

#### 並列ゲート実行

一部のゲートは並列実行可能：
- **Phase 3**: Methods+Results ペア ‖ Introduction+Conclusion ペア（Discussion は独立）
- **Phase 4**: 全セクションのヒューマナイズゲートを同時実行
- **Phase 6**: 全セクションレビューの後に quality-gate（順序依存）

Abstract のゲートは全セクション PASS 後に実行（他セクションの数値に依存するため）。

## Reference Files

- `references/imrad-guide.md` - IMRAD structure and writing principles
- `references/section-checklist.md` - per-section quality checklist (Original Article + Case Report)
- `references/citation-guide.md` - citation formatting and management
- `references/reporting-guidelines.md` - CONSORT, STROBE, PRISMA, CARE summaries
- `references/humanizer-academic.md` - AI writing pattern detection (EN 18 + VI 13 patterns)
- `templates/project-init.md` - project README template (Original Article)
- `templates/project-init-case.md` - project README template (Case Report)
- `templates/literature-matrix.md` - literature comparison matrix
- `templates/methods.md` - Methods section writing guide (Original Article)
- `templates/results.md` - Results section writing guide (Original Article)
- `templates/case-report.md` - Case presentation writing guide (Case Report, CARE-compliant)
- `templates/case-introduction.md` - Case Report introduction guide
- `templates/case-abstract.md` - Case Report abstract guide (CARE format)
- `templates/introduction.md` - Introduction section writing guide (Original Article)
- `templates/discussion.md` - Discussion section writing guide
- `templates/conclusion.md` - Conclusion writing guide
- `templates/abstract.md` - Abstract writing guide (Original Article)
- `templates/cover-letter.md` - Cover letter template
- `templates/submission-ready.md` - Pre-submission checklist template
- `templates/sr-outline.md` - Systematic review outline (PRISMA 2020)
- `templates/declarations.md` - Declarations templates (Ethics, COI, Funding, AI, CRediT)
- `templates/graphical-abstract.md` - Graphical abstract design guide
- `references/ai-disclosure.md` - AI tool disclosure guide (ICMJE 2023)
- `references/tables-figures-guide.md` - Tables and figures creation guide
- `references/keywords-guide.md` - Keywords and MeSH term selection guide
- `references/supplementary-materials.md` - Supplementary materials strategy guide
- `references/citation-verification.md` - Citation authenticity verification guide
- `references/pubmed-query-builder.md` - PubMed search query construction guide
- `templates/title-page.md` - Title page template (running head, ORCID, affiliations)
- `templates/highlights.md` - Key Points / Highlights / Summary boxes (VIMA, BMJ, Elsevier, etc.)
- `templates/limitations-guide.md` - Limitations section writing guide with templates
- `templates/acknowledgments.md` - Acknowledgments template (AI tools, medical writing)
- `templates/proof-correction.md` - Post-acceptance proof correction guide
- `references/submission-portals.md` - Submission portal guide (ScholarOne, Editorial Manager, etc.)
- `references/open-access-guide.md` - Open Access models, APCs, preprints, funder mandates
- `references/clinical-trial-registration.md` - Clinical trial registration guide (ClinicalTrials.gov, UMIN-CTR, jRCT)
- `references/abstract-formats.md` - Journal-specific abstract formats (VIMA, NEJM, Lancet, BMJ, etc.)
- `references/word-count-limits.md` - Word count limits by journal and paper type
- `references/coi-detailed.md` - Detailed COI categories, CRediT taxonomy, ORCID guide
- `references/desk-rejection-prevention.md` - Desk rejection prevention and journal selection
- `references/journal-reformatting.md` - Quick reformatting guide after rejection
- `references/statistical-reporting-full.md` - Extended SAMPL statistical reporting guide
- `references/reporting-guidelines-full.md` - Comprehensive reporting guidelines (20+ guidelines with checklists)
- `references/master-reference-list.md` - Master reference list with URLs (all resources)
- `templates/data-management.md` - Data management template (raw/processed/analysis, data dictionary, de-identification)
- `templates/analysis-workflow.md` - Data analysis workflow guide (Table 1, regression, survival, figures)
- `scripts/table1.py` - Table 1 generator (auto-detect variable types, normality test, group comparison)
- `scripts/analysis-template.py` - Statistical analysis template (descriptive, t-test, logistic, survival)


