Terraform Azure Infra CI/CD 🚀
📌 Overview
This repository contains Infrastructure-as-Code (IaC) using Terraform to provision Azure resources.
CI/CD automation is handled via GitHub Actions, ensuring safe deployments with branch-based control.

Feature branches → Run terraform plan and upload plan artifact.

Main branch → Download plan artifact and run terraform apply.

Node 24 → Default runtime for GitHub Actions (Node 20 deprecated).

⚙️ Workflow Summary
Steps in GitHub Actions:
Checkout repo

Setup Terraform

Terraform Init

Terraform Validate

Terraform Plan (feature branch only)

Upload Plan Artifact (feature branch only)

Download Plan Artifact (main branch only)

Terraform Apply (main branch only)

🛠️ Prerequisites
Azure subscription with required permissions.

GitHub repository secrets configured:

ARM_CLIENT_ID

ARM_CLIENT_SECRET

ARM_SUBSCRIPTION_ID

ARM_TENANT_ID

🚀 Usage
1. Run Plan (Feature Branch)
bash
git checkout -b feature/test-pipeline
git push origin feature/test-pipeline
This generates a plan and uploads the artifact (environment/tfplan).

2. Run Apply (Main Branch)
bash
git checkout main
git merge feature/test-pipeline
git push origin main
This downloads the plan artifact and applies it to Azure.

⚠️ Common Issues
Artifact not found → Ensure path: ./environment/tfplan is set in upload/download steps.

Resource already exists → Import existing resources into Terraform state:

bash
terraform import 'module.resource_group.azurerm_resource_group.adnan["rg1"]' /subscriptions/<sub_id>/resourceGroups/rg1
Node 20 warning → Ignore, Node 24 is default.

✅ Best Practices
Always run plan in feature branches before merging to main.

Use terraform import for existing Azure resources.

Keep secrets in GitHub → Settings → Secrets and variables → Actions.

Verify resources in Azure Portal after apply.
