# ☁️ AWS vs Azure — Comparative Analysis

![AWS](https://img.shields.io/badge/AWS-EC2%20%7C%20Lambda%20%7C%20EKS-orange?logo=amazonaws)
![Azure](https://img.shields.io/badge/Azure-VM%20%7C%20Functions%20%7C%20AKS-blue?logo=microsoftazure)
![Research](https://img.shields.io/badge/Type-Empirical%20Research-purple)
![License](https://img.shields.io/badge/License-MIT-green)

> **Hands-on empirical benchmarking of AWS vs Azure** across three cloud service layers — IaaS, FaaS, and CaaS — using real CLI experiments on live accounts. Raw data included for reproducibility.

---

## 📊 Key Results at a Glance

| Experiment | AWS | Azure | Winner |
|---|---|---|---|
| Windows VM Boot Time | 53.5 sec | 95.5 sec | **AWS** (44% faster) |
| Linux VM Boot Time | 156.5 sec | 63.1 sec | **Azure** (148% faster) |
| Serverless Cold Start | 628 ms | 621 ms | **TIE** |
| Serverless Cost (Python) | $0.00000145 | $0.00001700 | **AWS** (12× cheaper) |
| Kubernetes Provision Time | 13 min 11 sec | 5 min 21 sec | **Azure** (2.46× faster) |
| Kubernetes Control Plane Cost | $0.10/hr | FREE | **Azure** |

**Verdict:** Use **AWS Lambda** for serverless workloads. Use **Azure AKS** for Kubernetes.

---

## 🧪 Three Experiments

### Experiment 1 — VM Boot Time (IaaS)
- 20 × AWS EC2 t3.micro vs 20 × Azure Standard_D2s_v3
- Both Windows and Linux variants
- Raw data: [`04_Experimental_Data/EC2_Instance_Log_v5.xlsx`](04_Experimental_Data/EC2_Instance_Log_v5.xlsx)

### Experiment 2 — Serverless Cold Start & Cost (FaaS)
- 10 × AWS Lambda vs 10 × Azure Functions
- 6 runtimes: Node.js, Python, Java, .NET, Go, Ruby
- Raw data: [`04_Experimental_Data/Lambda_vs_AzureFunctions_Eval.xlsx`](04_Experimental_Data/Lambda_vs_AzureFunctions_Eval.xlsx)

### Experiment 3 — Kubernetes Provisioning (CaaS)
- 10 × AWS EKS vs 10 × Azure AKS clusters (K8s v1.34)
- Raw data: [`04_Experimental_Data/Cluster_Eval_EKS_vs_AKS.xlsx`](04_Experimental_Data/Cluster_Eval_EKS_vs_AKS.xlsx)

---

## 📁 Repository Structure

```
AWS-vs-Azure-Comparative-Analysis/
├── 02_Presentation/
│   └── Examiner_Cheat_Sheet.html     # Quick reference summary
├── 04_Experimental_Data/
│   ├── EC2_Instance_Log_v5.xlsx      # VM boot time raw data (20 runs each)
│   ├── Lambda_vs_AzureFunctions_Eval.xlsx  # Serverless raw data
│   └── Cluster_Eval_EKS_vs_AKS.xlsx # Kubernetes raw data
├── 05_References/
│   └── ref1 to ref18 *.txt / *.pdf  # 18 cited papers
└── 08_Session_Summary/
    ├── Session_Summary.md            # Full methodology notes
    └── AWS_Azure_Cleanup_Commands.md # CLI commands used
```

---

## 🔁 Reproduce the Experiments

```bash
# AWS CLI setup
aws configure
# Enter your Access Key, Secret, region (us-east-1 or ap-south-1)

# Azure CLI setup
az login
az account set --subscription YOUR_SUBSCRIPTION_ID
```

Full CLI commands in [`08_Session_Summary/AWS_Azure_Cleanup_Commands.md`](08_Session_Summary/AWS_Azure_Cleanup_Commands.md)

---

## 🎓 Use Cases

- ✅ Cloud computing research reference
- ✅ Final year project comparison data
- ✅ Architecture decision: AWS vs Azure
- ✅ Teaching material for cloud courses

---

## 📄 License

[MIT](LICENSE) — data and code free to use for research and education.
