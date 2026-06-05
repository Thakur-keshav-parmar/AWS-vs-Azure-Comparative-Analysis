# Complete Session Summary — AWS vs Azure Research + HardwarePro Report

**Date:** 2026  
**Session Tool:** Claude Code (Anthropic)

---

## What Was Accomplished

### Part A — HardwarePro MCA Project Report

1. **Started from:** `HardwarePro_Project_Report.docx` (4,445 KB original)
2. **Created versioned copies** (file_20 → file_21 → file_22) using Python + python-docx

**Transformations applied (fix_ptu_format.py → fix_ptu_v2.py):**
- Margins: Left 1", Top/Right/Bottom 1" (A4 PTU standard)
- Cover page: "PROJECT REPORT ON", "YOUR_UNIVERSITY_NAME", "YOUR_INSTITUTION_NAME
- Section headings added: STUDENT DECLARATION (On a Separate Page), FACULTY DECLARATION (On a Separate Page), ACKNOWLEDGEMENT (On a Separate Page), TABLE OF CONTENTS (On a Separate Page)
- TOC rebuilt: PTU 3-column table with black header, Student Declaration I/II/III, 9 chapters
- **Chapter 3 split:** 3.3 Objectives moved to new CHAPTER 4 (Features & Objectives)
- **Chapters renumbered:** original Ch4→5, Ch5→6, Ch6→7, Ch7→8, Ch8→9
- **Subsection numbers corrected:** all chapters 5-9 had wrong numbering (bug from renaming)
- **New sections added (file_22):**
  - 4.2 Key Features of HardwarePro (10 features)
  - 5.5 System Flowchart (full staff + admin flow)
  - 5.6 Data Flow Diagram — Level 0 + Level 1 (6 processes)
  - 5.7 Entity-Relationship Diagram (5 entities with full attributes)
  - 9.1 Limitations (10 detailed limitations before Conclusion)
- **Final file:** `file_22.docx` (4,251 KB) — in both project-report/ and research/ folders

**PTU Chapter Structure (Final):**
1. Synopsis
2. Introduction to the Project
3. Rationale, Need, Scope of the Project
4. Features and Objectives of the Project
5. Flowchart, DFD, ER Diagrams and Methodology
6. Technology Used and Data Analysis
7. Back End Tables, Implementations and Findings
8. Front End Forms, Interface and Testing
9. Limitations, Conclusion and Suggestions for Improvements

---

### Part B — AWS vs Azure Research Paper

**Starting file:** file-12.docx (research proposal, 18 references)

**Edits made (file-12 → file-13 → file-14):**
- **file-13:** Added Section 6 — Limitations of the Study (8 subsections 6.1–6.8)
- **file-14:** 
  - Renamed CONCLUSION → 7. CONCLUSION (numbered to match sections 1-6)
  - Removed informal conclusion text
  - Replaced with 5-paragraph IEEE-format conclusion with specific quantitative findings
  - Fixed Limitations heading: LIMITATIONS → 6. LIMITATIONS OF THE STUDY
  - Fixed subsection numbering throughout

**Final paper structure (file-14.docx / final(2).pdf):**
1. Introduction (1.1–1.3)
2. Research Objectives (2.1–2.2)
3. Literature Review (18 references table)
4. Research Methodology (4.1–4.5, 3 experiments with tables)
5. Results and Discussion (5.1–5.3)
6. Limitations of the Study (6.1–6.8)
7. Conclusion (5 paragraphs, IEEE format, citations)
8. References [1]–[18]

---

### Part C — Presentation (PPT)

**Tool:** python-pptx  
**File:** `AWS_Azure_PPT.pptx` (13 slides, ~91 KB)

**Slide structure (v2 — light theme):**
1. Title Slide (light theme, mixed AWS orange + Azure blue typography)
2. Introduction & Problem Statement
3. Research Objectives (3 objective cards)
4. Research Methodology & Setup
5. Experiment 1 — VM Boot Time (bar chart + stat boxes)
6. Experiment 2 — Serverless Cold Start (bar chart + runtime table)
7. Experiment 2 — Serverless Cost Per Invocation (bar chart + explanation)
8. Experiment 3 — Kubernetes Provision Time (10-run bar chart)
9. Experiment 3 — Kubernetes Cost Analysis (cost bar chart)
10. Overall Summary Table (12 metrics, 5-5-1 score)
11. Key Findings (3 finding cards)
12. Limitations (7 cards — first removed per user instruction)
13. Conclusion & Future Work

---

## Key Technical Bugs Fixed

| Bug | Root Cause | Fix |
|---|---|---|
| Chapter 4 re-renamed to 5 after split | New CHAPTER 4 element was found by subsequent rename search | Pre-collect all original chapter refs BEFORE any insertions |
| Chapter label + title appeared reversed | `addprevious()` ordering: inserting [A,B] in that order gives [A][B][ref] not [B][A][ref] | Remove `reversed()` from insertion loops |
| TOC table not found | Content-based matching missed "CONTENT" header | Iterate body XML directly for first `w:tbl` after TOC heading |
| UnicodeEncodeError in Python | cp1252 codec on Windows | Add `sys.stdout = io.TextIOWrapper(..., encoding='utf-8')` |
| `shape.line.fill.background()` failure | python-pptx API variation | Use lxml XML direct: `a:ln > a:noFill` |
| `chart.plot_area` AttributeError | Not available in python-pptx 1.2.0 | Remove those lines (white bg is default) |

---

## Files — What Was Kept vs Deleted

### Kept (Final Versions)
- `RESEARCH_FINAL/01_Research_Paper/AWS_Azure_Comparative_Analysis_FINAL.pdf`
- `RESEARCH_FINAL/02_Presentation/AWS_Azure_PPT_FINAL.pptx`
- `RESEARCH_FINAL/03_HardwarePro_Project_Report/HardwarePro_IMS_Report_FINAL.docx`
- `RESEARCH_FINAL/04_Experimental_Data/` — 3 xlsx workbooks + phase0 video
- `RESEARCH_FINAL/05_References/` — 18 reference PDFs/citation files
- `CREDENTIALS_KEEP_PRIVATE/AWS_AccessKeys_RESEARCH.csv` — KEEP SECURE

### Deleted (Intermediate Versions)
- `inventory management/project-report/file_20.docx` (original baseline copy)
- `inventory management/project-report/file_21.docx` (first PTU format edit)
- `research/Research_Proposal_AWS_vs_Azure_v2.docx` (earlier draft)

---

## AWS/Azure Resources — Research Experiments

See `AWS_Azure_Cleanup_Commands.md` for deletion commands.

Resources created during experiments:
- 10 AWS Lambda functions (lambda-node-basic, lambda-python-basic, etc.)
- 10 AWS EKS clusters (eks-eval-1 through eks-eval-10)
- 20 AWS EC2 t3.micro instances (likely already terminated)
- 10 Azure Function Apps
- 10 Azure AKS clusters (aks-eval-1 through aks-eval-10)
- 20 Azure Standard_D2s_v3 VMs (likely deallocated)

**HardwarePro production AWS resources — DO NOT DELETE.**

---

## Experimental Data Summary

### Experiment 1 — VM Boot Time
- File: `EC2_Instance_Log_v5.xlsx`
- AWS EC2 Windows avg: 53.5 sec | Azure VM Windows avg: 95.5 sec
- AWS EC2 Linux avg: 156.5 sec | Azure VM Linux avg: 63.1 sec

### Experiment 2 — Serverless
- File: `Lambda_vs_AzureFunctions_Eval.xlsx`
- Lambda avg cold start: 628ms | Azure avg cold start: 621ms
- Lambda Python cost: $0.00000145 | Azure Python: $0.00001700 (12x difference)

### Experiment 3 — Kubernetes
- File: `Cluster_Eval_EKS_vs_AKS.xlsx`
- EKS avg provision: 13 min 11 sec | AKS avg provision: 5 min 21 sec
- AKS is 2.46x faster; EKS charges $0.10/hr CP; AKS CP is FREE
