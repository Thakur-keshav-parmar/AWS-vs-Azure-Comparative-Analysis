# AWS & Azure Research Resource Cleanup Commands

Run these to delete all research-specific cloud resources and stop billing.
**Do NOT delete HardwarePro production resources.**

---

## AWS — Delete Research Resources

Open your terminal with AWS CLI configured (profile: research or default).

### 1. Delete Lambda Test Functions (10 research functions)
```bash
for fn in lambda-node-basic lambda-python-basic lambda-java-jvm lambda-dotnet-basic \
          lambda-go-basic lambda-node-vpc lambda-python-highmem lambda-ruby-basic \
          lambda-java-highmem lambda-node-container; do
  aws lambda delete-function --function-name $fn --region us-east-1
  echo "Deleted: $fn"
done
```

### 2. Delete EKS Clusters (10 research clusters)
```bash
for cluster in eks-eval-1 eks-eval-2 eks-eval-3 eks-eval-4 eks-eval-5 \
               eks-eval-6 eks-eval-7 eks-eval-8 eks-eval-9 eks-eval-10; do
  eksctl delete cluster --name $cluster --region us-east-1 --wait
  echo "Deleted: $cluster"
done
```

### 3. Check for any leftover EC2 instances (should already be terminated)
```bash
aws ec2 describe-instances \
  --filters "Name=instance-state-name,Values=running,stopped" \
  --query "Reservations[*].Instances[*].[InstanceId,Tags[?Key=='Name'].Value|[0],State.Name]" \
  --output table --region us-east-1
```
If any research instances appear, terminate them:
```bash
aws ec2 terminate-instances --instance-ids i-XXXXXXXXXX --region us-east-1
```

### 4. Check for leftover CloudWatch Log Groups
```bash
aws logs describe-log-groups --log-group-name-prefix /aws/lambda/lambda- \
  --query "logGroups[*].logGroupName" --output text --region us-east-1
```
Delete each:
```bash
aws logs delete-log-group --log-group-name /aws/lambda/lambda-node-basic --region us-east-1
```

### 5. Deactivate the Research IAM Access Key (research-cli_accessKeys.csv)
```bash
# First find the key ID from your CSV file, then deactivate it
aws iam update-access-key --access-key-id AKIAXXXXXXXXXXXXXXXX --status Inactive
aws iam delete-access-key --access-key-id AKIAXXXXXXXXXXXXXXXX
```

### 6. Remove local AWS CLI profile for research
```bash
aws configure --profile research
# Just press Enter 4 times to clear the values
# OR manually delete from: C:\Users\YOUR_USERNAME\.aws\credentials
```

---

## Azure — Delete Research Resources

### 1. Delete AKS Research Clusters & Resource Group
```bash
# Delete the AKS resource group (this deletes all clusters inside it)
az group delete --name <your-aks-resource-group> --yes --no-wait

# If clusters were in separate groups:
for i in 1 2 3 4 5 6 7 8 9 10; do
  az aks delete --name aks-eval-$i --resource-group <rg-name> --yes --no-wait
done
```

### 2. Delete Azure Function Apps
```bash
az functionapp list --query "[].{name:name, rg:resourceGroup}" --output table
# Delete each research function app:
az functionapp delete --name func-node-consumption --resource-group <rg-name>
az functionapp delete --name func-python-consumption --resource-group <rg-name>
# ... repeat for all 10 function apps
```

### 3. Delete Azure VMs (research VMs should already be deallocated)
```bash
az vm list --query "[].{name:name, rg:resourceGroup, state:powerState}" --output table
# Delete any remaining research VMs
az vm delete --name sample-1-windows --resource-group <rg-name> --yes
```

### 4. Delete the entire research resource group (easiest — deletes everything inside)
```bash
# Replace <research-rg> with the resource group you used for experiments
az group delete --name <research-rg> --yes --no-wait
```

### 5. Log out of Azure CLI
```bash
az logout
az account clear
```

---

## AWS CLI — Sign Out Locally
```powershell
# Clear stored credentials from Windows Credential Manager
Remove-Item "$env:USERPROFILE\.aws\credentials" -Force -ErrorAction SilentlyContinue
Remove-Item "$env:USERPROFILE\.aws\config" -Force -ErrorAction SilentlyContinue
Write-Host "AWS CLI credentials cleared."
```

---

## IMPORTANT — Do NOT Delete (HardwarePro Production)
The following AWS resources belong to the HardwarePro application and must NOT be deleted:
- DynamoDB tables: HardwareProProducts, HardwareProBills, HardwareProSuppliers, HardwareProPurchaseOrders, HardwareProUsers
- Lambda functions: All functions prefixed with `HardwarePro`
- S3 bucket: HardwarePro frontend bucket
- CloudFront distribution: E1XPPSNURZ2WPY
- API Gateway: HardwarePro API
- Cognito User Pool: HardwarePro auth

These are production resources for the HardwarePro Inventory Management System.
