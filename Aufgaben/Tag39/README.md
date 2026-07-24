# Individual Learning Phase – Azure CLI & Azure Automation

## Overview

In this lab, I learned how to automate basic Azure administration tasks using the **Azure CLI** and explored the fundamentals of **Azure Automation**. The exercise covered creating Azure resources, writing reusable CLI scripts, applying basic security practices, and introducing Runbooks for automated cloud operations.

---

## Objectives

- Configure and use Azure CLI
- Create Azure resources using CLI
- Build a reusable automation script
- Apply security best practices
- Explore Azure Automation and Runbooks

---

# Task 1 – Prepare Azure CLI

### Activities
- Logged into Azure using Azure CLI.
- Verified the active Azure subscription.
- Selected the correct subscription.
- Created a script file to document CLI commands.
- Chose a default Azure region.
- Defined a consistent naming convention.
- Verified permissions for resource creation.

### Result
Azure CLI was configured correctly and ready for resource deployment.

---

# Task 2 – Create Azure Resources

### Activities
- Created a new Resource Group.
- Created a Storage Account inside the Resource Group.
- Retrieved important resource properties:
  - Name
  - Location
  - SKU
  - Resource Group
- Documented all CLI commands with comments.

### Result
Successfully deployed Azure resources using Azure CLI.

---

# Task 3 – Create an Automation Script

### Activities
Created a reusable Bash script that:

- Defines variables for:
  - Resource Group
  - Location
  - Storage Account
- Checks whether the Resource Group already exists.
- Creates the Resource Group if necessary.
- Creates the Storage Account.
- Displays resource information after deployment.

### Security Considerations
- No passwords or secrets stored in the script.
- Uses variables instead of hardcoded values.

### Result
Successfully automated multiple Azure CLI commands in a single script.

---

# Task 4 – Improve Security

### Security Review

Checked the script for:

- Plain text credentials
- Access keys
- Connection strings
- Excessive permissions
- Unsafe delete commands
- Missing validation
- Missing comments

### Improvements

Implemented several improvements:

- Added existence checks before creating resources.
- Used variables instead of hardcoded values.
- Added comments for readability.
- Avoided storing secrets.
- Structured script output.

### Common Mistakes to Avoid

- Storing credentials in scripts
- Using overly broad permissions
- Deleting the wrong Resource Group
- Using duplicate Storage Account names

---

# Task 5 – Azure Automation

### Activities

Created an **Automation Account** and explored:

- Runbooks
- Jobs
- Variables
- Managed Identity

Created a basic Runbook for testing automation.

### Benefits of Azure Automation

- Executes directly in Azure.
- Supports scheduled execution.
- Reusable automation workflows.
- Uses Managed Identity for secure authentication.
- Eliminates dependency on a local computer.

---

# Extended Task 1 – Cleanup Script

Created a separate cleanup script that:

- Prompts for confirmation before deletion.
- Deletes only the Resource Group created for the lab.
- Prevents accidental removal of unrelated resources.

---

# Extended Task 2 – Runbook Concept

Example automation idea:

**Task**

Verify that required Storage Accounts exist.

**Trigger**

- Scheduled execution
- Manual execution

**Required Permissions**

- Contributor on the target Resource Group

**Risk**

Avoid assigning Owner permissions unless absolutely necessary.

---

# Extended Task 3 – Script Improvements

Added additional robustness by:

- Validating resource names.
- Checking Azure login status.
- Verifying the selected subscription.
- Separating configuration from execution.
- Improving script comments and documentation.

---

# Security Best Practices

- Never store passwords or secrets in scripts.
- Follow the Principle of Least Privilege.
- Validate resources before creation or deletion.
- Use globally unique Storage Account names.
- Review commands before executing delete operations.

---

# Reflection

## What can be standardized?

- Resource Group creation
- Storage Account deployment
- Resource validation
- Environment setup

## Why use scripts?

Scripts reduce manual work, improve consistency, and allow repeatable deployments.

## Why avoid storing credentials?

Stored credentials can be exposed and lead to unauthorized access.

## When is Azure Automation better?

Azure Automation is ideal for scheduled, recurring, and cloud-native administrative tasks.

## Recommended minimum permissions

Contributor access limited to the required Resource Group.

## Future Improvements

- Better error handling
- Logging
- Input validation
- Parameterized scripts
- Reusable automation modules

---

# Conclusion

This lab demonstrated how Azure CLI can automate common administrative tasks while following security best practices. It also introduced Azure Automation as a scalable solution for scheduling and managing recurring cloud operations through Runbooks and Managed Identities.
