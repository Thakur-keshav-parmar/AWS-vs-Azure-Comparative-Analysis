# AWS vs Azure Comparative Analysis — Research Archive

**Topic:** Comparative Analysis of Compute Services of AWS & Azure  
**Level:** Postgraduate Research (Cloud Computing)  
**Completed:** 2026

---

## Folder Structure

| Folder | Contents |
|---|---|
| `01_Research_Paper/` | Final research paper + proposal |
| `02_Presentation/` | Final PPT (13 slides) + examiner reference sheet |
| `04_Experimental_Data/` | Excel workbooks (EC2 logs, Lambda data, EKS/AKS timings) |
| `05_References/` | All 18 reference PDFs and citation text files |
| `06_Supporting_Documents/` | Step-by-step walkthrough, setup notes, research guide |
| `08_Session_Summary/` | Full session notes, decisions log, AWS/Azure cleanup commands |

---

## Research Summary

**Title:** Comparative Analysis of Compute Services of AWS & Azure

**Abstract:** Hands-on empirical benchmarking of AWS and Azure across three cloud service layers
(IaaS, FaaS, CaaS) using real CLI-based experiments on live accounts.

**3 Experiments:**
1. **VM Boot Time** — 20 EC2 t3.micro vs 20 Azure D2s_v3 VMs (Windows + Linux)
2. **Serverless Cold Start & Cost** — 10 Lambda vs 10 Azure Functions (6 runtimes)
3. **Kubernetes Provisioning** — 10 EKS vs 10 AKS clusters (K8s v1.34)

**Key Results:**

| Metric | Winner | Margin |
|---|---|---|
| Windows VM Boot | AWS EC2 | 44% faster (53.5s vs 95.5s) |
| Linux VM Boot | Azure VM | 148% faster (63.1s vs 156.5s) |
| Cold Start Latency | TIE | 628ms vs 621ms |
| Serverless Cost | AWS Lambda | Up to 12× cheaper |
| K8s Provision Speed | Azure AKS | 2.46× faster (5m21s vs 13m11s) |
| K8s Control Plane Cost | Azure AKS | FREE vs $0.10/hr |

**Verdict:** Hybrid strategy — AWS Lambda for serverless, Azure AKS for Kubernetes.

---

## How to Use This Repository

- **Researchers** — Use the experimental data in `04_Experimental_Data/` for comparison benchmarks
- **Students** — Reference methodology in `01_Research_Paper/` and `06_Supporting_Documents/`
- **Practitioners** — See `08_Session_Summary/AWS_Azure_Cleanup_Commands.md` for real CLI workflows

---

## Reproduce the Experiments

All experiments were run using free-tier / pay-as-you-go AWS and Azure accounts via CLI.  
No special access required. See `06_Supporting_Documents/` for step-by-step guides.

**AWS services used:** EC2, Lambda, EKS, CloudWatch  
**Azure services used:** Virtual Machines, Azure Functions, AKS, Monitor
