# CLAUDE CODE PROMPT

**Copy and paste this entire prompt into Claude Code or Claude Desktop with code execution enabled.**

---

## TASK: TLID_deep_interpretation_and_high_standard_redraft

### INPUT:

```yaml
zip_path: "Dengue_TLID_Submission_Ready_Pack_v3.zip"
```

---

## NON-NEGOTIABLE RULES:

1. **Do not invent** numbers, citations, cohorts, outcomes, or methods.
2. **Every numeric or factual claim** must be traceable to an artifact inside the ZIP.
3. **If a claim is not traceable**: delete it or rewrite as an explicit **GAP** / "Not reported".
4. **Do not add** new figures or analyses not present in the ZIP.
5. **Maintain an auditable trail**: preflight report, claim ledger, interpretation memo, and section-by-section diff.

---

## EXECUTION STEPS:

### 1) Unzip → verify folder tree → write `00_Preflight_Report.md`

- Extract `Dengue_TLID_Submission_Ready_Pack_v3.zip` into `workdir/`
- Verify exact folder structure:
  ```
  0_Cover_Letter/
  1_Manuscript/
  2_Main_Figures/
  3_Supplementary_Figures/
  4_Supplementary_Data/
  ```
- List all files with names and sizes
- If `Manifest.json` + `Hashes.txt` exist: verify hashes
- If hashes not available: register "hash verification not available in this pack" (without inventing)

**Output**: `01_audit_outputs/00_Preflight_Report.md`

---

### 2) Build `01_Claim_Ledger.tsv` mapping each claim to exact artifact + location

**Structure**:

| Claim_ID | Claim_Text | Artifact | Location | Gate0_Status | Allowed_Wording | Forbidden_Wording | Notes |
|----------|------------|----------|----------|--------------|-----------------|-------------------|-------|

**Rules**:

- Every number (conteos, N, AUC, CI) must be traced
- If AUC/CI from figure → must be confirmed by table/data
- "Only candidate with prospective external validation" → only if `Evidence_Table_MASTER.csv` supports it

**Output**: `01_audit_outputs/01_Claim_Ledger.tsv`

---

### 3) Write `02_Interpretation_Memo.md` using **only ledger-supported claims**

**Structure** (TLID-friendly):

1. **Evidential architecture**
   - What is "candidate", what enters/exits (prognosis vs forecasting vs associative)
   - What Gate 0 does and why it changes the field

2. **Landscape diagnosis (attrition + heterogeneity)**
   - PRISMA counts (2415 → 57 → 55 + 2 excluded) and what it means
   - Dominant bias: retrospective, single-center, no external validation

3. **Benchmark appraisal**
   - **Liu 2022**: what it actually proves (discrimination), what it doesn't (calibration), and what this implies (local recalibration)
   - **Robinson 2019**: why it's a comparator but with "optimism risk" (small N)

4. **Quality & bias envelope**
   - PROBAST summary by domains (without exaggeration)
   - TRIPOD: critical absences typical (calibration, complete model, transparency)

5. **Anchors meta-evidence**
   - Platelets and AST/ALT as robust signals: **only if** supported by anchors/meta-evidence file included
   - Differentiate: "consistent directional association" ≠ "deployable prognostic model"

6. **No-go list** (what CANNOT be affirmed)
   - "Ready for deployment" (prohibited if no calibration + clinical impact + DCA, etc.)
   - "Best model" (prohibited: only "audited benchmark")
   - "Omics beyond transcriptomics are inferior" (prohibited if no traceable comparison)

**Output**: `01_audit_outputs/02_Interpretation_Memo.md`

---

### 4) Write `03_Omics_Gap_Note.md` explaining why only transcriptomic coherence figure is justified

**TLID editorial rule**:

If there are **no multivariable metabolomics/proteomics models with Gate0 PASS and external validation**, then:

- **Do not** build a multi-omic mechanistic figure "as if evidence existed"
- Write as **gap**: "non-transcriptomic multi-omic prognostic models lacked traceable, externally validated candidates within the audited set" (always traced)

**Output** (`03_Omics_Gap_Note.md` - 1 page):

- What omics appeared in the landscape (if `Evidence_Table_MASTER.csv` allows)
- How many pass Gate0
- How many have external validation
- **Conclusion**: why they weren't included in Figure 3

**Output**: `01_audit_outputs/03_Omics_Gap_Note.md`

---

### 5) Redraft manuscript to TLID style:

**Keep PRISMA + Gate0 governance prominent**:

- Enforce defensive wording (benchmark = audited benchmark; calibration = gap)
- Insert figure callouts in Results 2.1/2.2 and Discussion plausibility

**TLID narrative structure** (what TLID rewards):

1. **What real problem you solve**
   - Not "another systematic review", but: integrity audit that separates prognosis from noise and ghost evidence

2. **What you contribute**
   - Gate 0 + pipeline + audited benchmark

3. **What changes**
   - Implications for policy and design of future models (calibration + validation + traceability)

**TLID style checklist**:

- ✅ Short sentences. Active verbs.
- ✅ Zero hype.
- ✅ "We audited / We verified / We excluded" (operational).
- ✅ **Explicit limitations**: calibration not reported; heterogeneity; low N of validation.

**Output**: `02_redraft/Manuscript_Dengue_SR_TLID_FINAL.docx`

---

### 6) Output:

- `02_redraft/Manuscript_Dengue_SR_TLID_FINAL.docx`
- `02_redraft/04_Section_by_Section_Diff.md` (what changed and why)
- `02_redraft/05_Final_QC_Checklist.md` with:
  - PRISMA counts consistent throughout text
  - Table 1 consistent with Results
  - Limitations written
  - Complete declarations
  - References/citations coherent (no broken keys)

---

## QUALITY BAR:

- ❌ No unsupported superlatives (first/best/ready-to-deploy) unless proven in ledger
- ✅ Explicitly separate **discrimination vs calibration**
- ✅ Explicitly quantify **integrity exclusions** and define **ghost evidence**
- ✅ Explain **limitations** and **policy implications** without overreach

---

## DIRECT RESPONSE TO THE OMICS QUESTION:

**"Why is Figure 3 transcriptomics-only?"**

**Correct answer** (and TLID will reward it) — always traced:

- **Figure 3 exists** because the only auditable benchmark with prospective external validation is transcriptomic (and the comparator too).
- The other omics, if they don't have **Gate0 PASS candidates + external validation + complete extraction**, are treated as **"gap"** and that's it.
- If you want, you can later add **S4 "Omics Landscape"** (not mechanistic; only presence/absence map and Gate0/validation status), but **only if** `Evidence_Table_MASTER.csv` allows counting by omic.

---

## FINAL NOTE:

If you want, I can prepare the exact text (2–3 sentences) to embed in Discussion about the "omics gap" in TLID tone, but first Claude Code must confirm in the ledger:

- What omics appear
- With what status (Gate0/validation)

---

**END OF PROMPT**

---

## How to use this prompt:

1. Copy this entire file
2. Paste into **Claude Code** or **Claude Desktop** with code execution enabled
3. Ensure `Dengue_TLID_Submission_Ready_Pack_v3.zip` is in your working directory or specify correct path
4. Let Claude Code execute all steps sequentially
5. Review outputs in `01_audit_outputs/` and `02_redraft/` folders

---

**Contact**: Elkin Navarro Quiroz (`elkin.navarro@unisimonbolivar.edu.co`)
