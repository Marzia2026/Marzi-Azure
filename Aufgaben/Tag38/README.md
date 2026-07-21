
# Individual Learning Phase: PowerShell Scripting Fundamentals in Azure

## Objective

The objective of this exercise is to learn the fundamentals of Azure automation using PowerShell. The scripts demonstrate the use of variables, arrays, hashtables, conditions, loops, reporting, parameterization, and validation while managing Azure Resource Groups.

---

# Task 1 – Prepare the Script Environment

## Objective
Prepare the PowerShell environment and verify the Azure connection.

### Script: `01-setup.ps1`

```powershell
Write-Host "===== Azure Environment Check ====="

Write-Host "PowerShell Version:" $PSVersionTable.PSVersion
Write-Host "Current Date/Time:" (Get-Date)

try {
    $context = Get-AzContext -ErrorAction Stop
}
catch {
    Connect-AzAccount
    $context = Get-AzContext
}

Write-Host "Account      :" $context.Account
Write-Host "Tenant       :" $context.Tenant.Id
Write-Host "Subscription :" $context.Subscription.Name

Write-Host "Environment is ready!"
```

### Result

- Displays PowerShell version.
- Displays current date and time.
- Shows Azure account, tenant, and subscription.
- Confirms that the environment is ready.

---

# Task 2 – Create Variables and Data Structures

## Objective

Create variables, arrays, and hashtables to plan Azure Resource Groups.

### Script: `02-planung.ps1`

```powershell
$Prefix = "abc2407"
$Region = "westeurope"
$Environment = "dev"

$Workloads = @(
    "app",
    "data",
    "monitor"
)

$Tags = @{
    Owner       = "Ali"
    Environment = $Environment
    Training    = "ILP"
}

foreach ($Workload in $Workloads) {
    $RGName = "$Prefix-$Environment-$Workload-rg"
    Write-Host $RGName
}

$Tags
```

### Result

- Defines reusable variables.
- Stores workloads in an array.
- Stores Azure tags in a hashtable.
- Automatically generates Resource Group names.

---

# Task 3 – Safe Resource Group Creation

## Objective

Prevent duplicate Resource Group creation.

### Script: `03-rg-check.ps1`

```powershell
foreach ($Workload in $Workloads) {

    $RGName = "$Prefix-$Environment-$Workload-rg"

    $RG = Get-AzResourceGroup -Name $RGName -ErrorAction SilentlyContinue

    if ($RG) {

        Write-Host "$RGName already exists."

    }
    else {

        New-AzResourceGroup `
            -Name $RGName `
            -Location $Region `
            -Tag $Tags

        Write-Host "$RGName created."

    }

}
```

### Result

- Checks whether a Resource Group already exists.
- Creates only missing Resource Groups.
- Prevents duplicate resources.

---

# Task 4 – Automate Multiple Resource Groups

## Objective

Process multiple Resource Groups automatically.

### Extended Script

```powershell
$Created = 0
$Existing = 0

foreach ($Workload in $Workloads) {

    $RGName = "$Prefix-$Environment-$Workload-rg"

    if (Get-AzResourceGroup -Name $RGName -ErrorAction SilentlyContinue) {

        $Existing++
        Write-Host "$RGName already exists."

    }
    else {

        New-AzResourceGroup `
            -Name $RGName `
            -Location $Region `
            -Tag $Tags

        $Created++
        Write-Host "$RGName created."

    }

}

Write-Host ""
Write-Host "========== Summary =========="
Write-Host "Created : $Created"
Write-Host "Existing: $Existing"
```

### Result

- Uses a `foreach` loop.
- Processes all workloads automatically.
- Displays a summary of created and existing Resource Groups.

---

# Task 5 – Reporting and Cleanup

## Objective

Generate a report and optionally remove test Resource Groups.

### Script: `04-report-cleanup.ps1`

```powershell
$Cleanup = $false
$Prefix = "abc2407"

$Groups = Get-AzResourceGroup |
Where-Object {
    $_.ResourceGroupName -like "$Prefix*" -or
    $_.Tags["Training"] -eq "ILP"
}

$Groups |
Select-Object ResourceGroupName, Location, ProvisioningState, Tags |
Export-Csv "ResourceGroupReport.csv" -NoTypeInformation

if ($Cleanup) {

    foreach ($RG in $Groups) {

        Remove-AzResourceGroup `
            -Name $RG.ResourceGroupName `
            -Force

    }

}
else {

    Write-Host "Cleanup disabled."

}
```

### Result

- Generates a CSV inventory report.
- Lists Resource Groups matching the prefix or Training tag.
- Cleanup is disabled by default for safety.

---

# Extension Task 1 – Parameterization

```powershell
param(

[string]$Prefix,

[string]$Region,

[string]$Environment,

[string[]]$Workloads

)
```

Example:

```powershell
.\03-rg-check.ps1 `
-Prefix demo01 `
-Region westeurope `
-Environment dev `
-Workloads app,data,monitor
```

### Result

The script becomes reusable without editing the source code.

---

# Extension Task 2 – Input Validation

```powershell
if ([string]::IsNullOrWhiteSpace($Prefix)) {
    throw "Prefix cannot be empty."
}

if ($Workloads.Count -eq 0) {
    throw "At least one workload is required."
}

$ValidRegions = (Get-AzLocation).Location

if ($Region -notin $ValidRegions) {
    throw "Invalid Azure region."
}
```

### Result

- Prevents invalid user input.
- Stops execution with meaningful error messages.

---

# Extension Task 3 – Azure Inventory

### Script: `05-inventar.ps1`

```powershell
$Inventory = Get-AzResourceGroup

Write-Host "Total Resource Groups:"
Write-Host $Inventory.Count

$Inventory |
Group-Object Location |
Format-Table Name, Count

$Inventory |
Where-Object {
    $_.Tags["Owner"] -eq $null
} |
Select ResourceGroupName, Location

$Inventory |
Export-Csv AzureInventory.csv -NoTypeInformation
```

### Result

- Counts all Resource Groups.
- Groups them by Azure region.
- Finds Resource Groups without an Owner tag.
- Saves the inventory as a CSV file.

---

# Reflection

## 1. Where did you effectively use variables, arrays, and hashtables?

Variables stored reusable values such as Prefix, Region, and Environment. Arrays stored multiple workloads, while hashtables were used to manage Azure tags efficiently.

## 2. How did the if/else condition help?

The condition checked whether a Resource Group already existed before creation, preventing duplicate resources and unnecessary errors.

## 3. Which recurring Azure task was simplified with a loop?

Using a `foreach` loop automated the creation, checking, reporting, and cleanup of multiple Resource Groups without repeating code.

## 4. How could the script be extended for another subscription?

The script can be parameterized further by adding a Subscription ID parameter and using `Set-AzContext` to switch subscriptions before execution.

## 5. Which output messages were most useful?

Messages indicating Resource Group creation, existing resources, validation results, and the final summary provided a clear understanding of the execution flow.

---

# Conclusion

This learning phase successfully demonstrates the core PowerShell scripting concepts for Azure automation, including:

- Azure authentication and environment setup
- Variables, arrays, and hashtables
- Conditional logic (`if/else`)
- Loop automation (`foreach`)
- Azure Resource Group management
- Reporting and cleanup
- Parameterization and validation
- Azure inventory generation

These scripts provide a reusable foundation for automating Azure administrative tasks using PowerShell.
