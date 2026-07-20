
# Azure CLI – First Steps

This lab focused on learning the fundamentals of **Azure CLI** by configuring the environment, managing Azure resources, and comparing Azure CLI with Azure PowerShell.

## Objectives

- Install and verify Azure CLI
- Sign in to Azure and configure the active subscription
- Create and manage a Resource Group
- Deploy and inspect an Azure Storage Account
- Compare Azure CLI commands with Azure PowerShell
- Practice output formatting, filtering, and resource cleanup

---

## Environment

- **Platform:** Windows 11
- **Terminal:** Windows Terminal (PowerShell)
- **Tool:** Azure CLI
- **Azure Subscription:** Personal/Test Subscription

---

## Tasks Completed

### 1. Azure CLI Setup

- Verified Azure CLI installation
- Checked CLI version using:
  ```bash
  az --version
  ```

### 2. Authentication & Configuration

- Signed in to Azure
- Listed available subscriptions
- Selected the working subscription
- Configured default values (Location / Resource Group)

Key commands:

```bash
az login
az account list
az account set
az account show
az configure --defaults
```

---

### 3. Resource Group Management

- Created a new Resource Group
- Listed existing Resource Groups
- Queried the new Resource Group
- Added metadata tags
- Displayed Resource Group details

Example tags:

- Project
- Environment
- Owner

---

### 4. Storage Account Deployment

- Created a globally unique Storage Account
- Used **Standard_LRS** SKU
- Verified deployment
- Listed Storage Accounts
- Inspected endpoints and security-related settings

---

### 5. Azure CLI vs Azure PowerShell

| Task | Azure CLI | PowerShell |
|------|-----------|------------|
| List Resource Groups | `az group list` | `Get-AzResourceGroup` |
| Show Resource Group | `az group show` | `Get-AzResourceGroup -Name` |
| Show Storage Account | `az storage account show` | `Get-AzStorageAccount` |

### Comparison

**Azure CLI**

- Short and concise syntax
- Cross-platform (Windows, Linux, macOS)
- Excellent for automation and DevOps

**Azure PowerShell**

- Object-oriented output
- Better integration with PowerShell scripting
- More suitable for complex administrative automation

---

## Extension Tasks

Completed additional exercises including:

- Displaying resources in **Table** and **JSON** formats
- Filtering output using **JMESPath queries**
- Querying Azure regions
- Updating resource tags
- Cleaning up resources to avoid unnecessary costs

---

## Key Azure CLI Commands Learned

```bash
az login
az account list
az account set
az configure --defaults
az group create
az group list
az group show
az group update
az storage account create
az storage account list
az storage account show
az group delete
```

---

## Lessons Learned

- Azure CLI provides a fast and efficient way to manage Azure resources.
- Default configuration simplifies repetitive commands.
- Resource tagging improves organization and governance.
- Storage Account names must be globally unique.
- Azure CLI is ideal for automation, while PowerShell is better for advanced scripting.

---

## Reflection

After completing this lab, I can confidently:

- Configure Azure CLI
- Manage Azure subscriptions
- Create and maintain Resource Groups
- Deploy and inspect Azure Storage Accounts
- Compare Azure CLI with Azure PowerShell
- Format and filter Azure CLI output
- Clean up Azure resources to minimize costs
