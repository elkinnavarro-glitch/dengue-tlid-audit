# dengue-tlid-audit

**Dengue Systematic Review: TLID Redrafting Repository**

---

## Repository Structure

```
dengue-tlid-audit/
├── README.md                     # This file
├── CLAUDE_CODE_PROMPT.md         # Copy-paste prompt for Claude Code
├── LICENSE                       # MIT or CC-BY-4.0
├── 00_input/                     # Raw submission pack
│   ├── Cover_Letter.docx
│   ├── Manuscript_Dengue_SR.docx
│   ├── Supplementary_Legends.docx
│   ├── PRISMA_counts.json
│   ├── TRIPOD_matrix.csv
│   ├── PROBAST_matrix.csv
│   ├── Evidence_Table_MASTER.csv
│   ├── Figure_S1_PRISMA.pdf
│   └── Figure_S2_Governance.pdf
├── 01_audit_outputs/             # Traceability artifacts
│   ├── 00_Preflight_Report.md
│   ├── 01_Claim_Ledger.tsv
│   ├── 02_Interpretation_Memo.md
│   ├── 03_Omics_Gap_Note.md
│   └── logs/
│       └── verification_timestamps.json
├── 02_redraft/                   # Final TLID-ready manuscript
│   ├── Manuscript_Dengue_SR_TLID_FINAL.docx
│   ├── 04_Section_by_Section_Diff.md
│   └── 05_Final_QC_Checklist.md
└── scripts/                      # Optional automation helpers
    └── doi_verifier.py           # If you want to reproduce Gate0
```

---

## Mission Statement

This repository contains the **evidence audit** and **TLID-compliant redrafting workflow** for the dengue prognostic models systematic review.

### Core principles:

1. **No fabrication**: Every claim is traceable to an artifact in `00_input/`.
2. **Defensive wording**: `discrimination ≠ calibration`, `benchmark ≠ deployment-ready`.
3. **Explicit gaps**: "Calibration not reported"; "multi-omic candidates lacked external validation".
4. **Auditable trail**: Claim Ledger → Interpretation Memo → Section diffs.

---

## Quick Start for Claude Code

### Step 1: Clone and populate input

```bash
git clone https://github.com/elkinnavarro-glitch/dengue-tlid-audit.git
cd dengue-tlid-audit
```

Place all submission files in `00_input/`

### Step 2: Execute audit + redraft

Open `CLAUDE_CODE_PROMPT.md` and paste the full prompt into **Claude Code** or **Claude Desktop** with code execution.

Claude Code will:

1. Verify folder structure → `00_Preflight_Report.md`
2. Build claim-to-artifact ledger → `01_Claim_Ledger.tsv`
3. Generate interpretation memo → `02_Interpretation_Memo.md`
4. Explain omics gap → `03_Omics_Gap_Note.md`
5. Redraft manuscript to TLID standards
6. Output section-by-section diff and QC checklist

---

## Audit Architecture

### A. Gate 0 Philosophy

**Definition**: A study passes Gate 0 if:

- **DOI** resolves to canonical publisher record
- **Metadata** (title, year, journal) matches
- **Methods** are traceable and reproducible

**Consequence**: 2 candidates excluded as "ghost evidence" despite grey literature citations.

---

### B. Claim Ledger Structure

| Column | Description |
|--------|-------------|
| `Claim_ID` | Unique identifier (C001, C002...) |
| `Claim_Text` | The exact statement in manuscript |
| `Artifact` | Source file name (`Evidence_Table_MASTER.csv`, `PRISMA_counts.json`, etc.) |
| `Location` | Row/column or section identifier |
| `Gate0_Status` | PASS / FAIL / NA |
| `Allowed_Wording` | How to phrase for TLID |
| `Forbidden_Wording` | What NOT to say |
| `Notes` | Gaps, uncertainties, biases |

#### Example row:

| Claim_ID | Claim_Text | Artifact | Location | Gate0_Status | Allowed_Wording | Forbidden_Wording | Notes |
|----------|------------|----------|----------|--------------|-----------------|-------------------|-------|
| C001 | "Liu et al. 2022 is the only candidate with prospective external validation" | `Evidence_Table_MASTER.csv` | R0001, `ext_validation=yes`, `ext_val_country=Colombia` | PASS | "Liu 2022 is the only audited model with prospective external validation" | "Liu 2022 is deployment-ready" | Calibration not reported; requires local recalibration |

---

### C. Interpretation Memo Sections

1. **Evidential architecture**: What is a "candidate" vs "associative study" vs "forecasting model"
2. **Landscape diagnosis**: PRISMA flow (2415→57→55), attrition analysis
3. **Benchmark appraisal**: Liu 2022 (what it proves and what it doesn't), Robinson 2019 (comparator with optimism risk)
4. **Quality envelope**: PROBAST/TRIPOD summaries, no exaggeration
5. **Meta-evidence anchors**: Platelets, AST/ALT → directional signals
6. **No-go list**: Explicit prohibitions ("ready-to-deploy", "best model", "omics superiority claims")

---

### D. Omics Gap Rationale

**Question**: Why is Figure 3 transcriptomics-only?

**Answer (traceable)**:

- **Liu 2022**: 8-gene transcriptomic, external prospective validation, Gate0 PASS
- **Robinson 2019**: 20-gene transcriptomic, external prospective validation, Gate0 PASS, but N=34
- **Metabolomics candidates** (R0005, R0021): No external validation with Gate0 PASS
- **Proteomics candidates** (R0025, R0026): Internal only or unverified validation
- **Lipidomics/genomics**: Association studies, not multivariable prognostic models

**Conclusion**: "Non-transcriptomic multi-omic prognostic models lacked traceable, externally validated candidates within the audited set."

---

## TLID Editorial Alignment

### What TLID values:

| Element | Our Approach |
|---------|-------------|
| **Real-world impact** | Gate 0 separates deployable evidence from noise |
| **Methodological rigor** | PROBAST + TRIPOD + integrity pipeline |
| **Explicit limitations** | Calibration gap, small N, heterogeneity |
| **Policy implications** | Prioritize verifiable benchmarks over volume |
| **Transparency** | Full audit trail (ledger, logs, diffs) |

### TLID Style Checklist:

- ✅ Short sentences, active voice
- ✅ Operationalize verbs ("We audited", "verified", "excluded")
- ✅ No hype ("benchmark" not "breakthrough")
- ✅ Explicit gaps ("calibration not reported")
- ✅ Figure callouts in Results 2.1/2.2 and Discussion
- ✅ Limitations section complete
- ✅ Declarations (funding, conflicts, data availability)

---

## Usage Notes

### For Claude Code:

The full execution prompt is in `CLAUDE_CODE_PROMPT.md`.

**Key parameters**:

```yaml
NON_NEGOTIABLE_RULES:
  - Do not invent numbers, citations, cohorts, outcomes, methods
  - Every claim must trace to an artifact in 00_input/
  - If not traceable → delete or rewrite as explicit GAP
  - Maintain auditable trail (preflight, ledger, memo, diff)
```

### After Claude Code execution:

1. Read `02_Interpretation_Memo.md` (the "brain" of the paper)
2. Check `01_Claim_Ledger.tsv` for any red flags
3. Review `04_Section_by_Section_Diff.md` to see what changed and why
4. Validate `05_Final_QC_Checklist.md` against TLID submission requirements
5. If satisfied, use `Manuscript_Dengue_SR_TLID_FINAL.docx` for submission

---

## For Human Reviewers

This is a **single-project audit repository**. For methodological questions or adaptation to other systematic reviews, contact:

**Elkin Navarro Quiroz**  
`elkin.navarro@unisimonbolivar.edu.co`  
CICV, Universidad Simón Bolívar, Barranquilla, Colombia

---

## Contributing

Not accepting external contributions (single-project audit).

---

## License

- **MIT License** for code/scripts  
- **CC-BY-4.0** for documentation and interpretation memos

---

## Citation

If you adapt this pipeline for your own systematic review:

```bibtex
@misc{dengue_tlid_audit_2026,
  author = {Navarro Quiroz, Elkin and collaborators},
  title = {Dengue Systematic Review: Integrity Audit and TLID Redrafting Pipeline},
  year = {2026},
  url = {https://github.com/elkinnavarro-glitch/dengue-tlid-audit},
  note = {Evidence governance workflow for high-impact journal submission}
}
```

---

## Changelog

### 2026-02-02 (v1.0)

- Initial repository structure
- Claude Code prompt formalized
- Input pack uploaded (Cover Letter, Manuscript, Tables, Figures, Logs)
- Audit outputs scaffolded
- TLID alignment documented

---

## Troubleshooting

**For technical issues with Claude Code execution**:  
Check that all files in `00_input/` match expected names and formats.

**For scientific/methodological questions**:  
Refer to `02_Interpretation_Memo.md` for the complete reasoning chain.

**For TLID editorial alignment**:  
Cross-reference `05_Final_QC_Checklist.md` with TLID author guidelines.

---

**End of README**

---

## Contact

**Elkin Navarro Quiroz**  
`elkin.navarro@unisimonbolivar.edu.co`
