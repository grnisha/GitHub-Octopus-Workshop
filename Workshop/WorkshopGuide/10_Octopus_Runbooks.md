#  Octopus Runbook Configuration

[Octopus Deploy Runbooks](https://octopus.com/docs/runbooks) is a way to automate routine maintenance and emergency operations tasks, such as infrastructure provisioning, database management, and website failover and restoration.

In this section, we'll detail how to set up your Infrastructure using Infrastructure as Code, and we'll provision all resources automatically using Octopus Runbooks. 


## Creating Infrastructure

In this section, we'll go through the configuration of spinning up all your Infrastructure as Code using Octopus Runbooks. 

### Creating Resource Group

In this step, we create the [Azure Resource Group](https://docs.microsoft.com/azure/azure-resource-manager/management/manage-resource-groups-portal). 

- Browse your RandomQuotes project
- Select **Runbooks** under **Operations**
- Select **Add Runbook**
- Input the name of **Create Infrastructure** and select **Save**
- Go to **Process** and select **Add Step** and search for **Run an Azure Script**
- Name this step **Create an Azure Resource Group**
- Set the execution location to **Run once on a worker**
- Ensure the **Default worker pool** is selected
- Ensure **User Azure tools bundled with Octopus** is selected within the **Azure Tools** section
- Please bind **#{Azure.Account.Name}** to the Azure Account. 
- Within the Inline Source Code section select **PowerShell** and paste in the following code:

```powershell
## This step creates the Resource Group within Azure if it doesn't already exist. 

$resourceGroupName = $OctopusParameters["Azure.ResourceGroup.Name"]
$resourceGroupLocation = $OctopusParameters["Azure.Location.Abbr"]

Try {
	Get-AzureRmResourceGroup -Name $resourceGroupName
    $createResourceGroup = $false
} Catch {
	$createResourceGroup = $true
}

if ($createResourceGroup -eq $true){
	New-AzureRmResourceGroup -Name $resourceGroupName -Location $resourceGroupLocation
}
```

- Now click on **Save**


### Create App Service Plan

In this step, we create the [Azure App Service Plan](https://docs.microsoft.com/azure/app-service/)

- In the Runbook, go to **Process** and select **Add Step** and search for **Deploy an Azure Resource Manager template** 
- Name this step **Deploy Azure App Service Plan**
- Set the execution location to **Run once on a worker**
- Ensure the **Default worker pool** is selected
- Ensure **User Azure Tools pre-installed on the worker** is selected
- Please bind **#{Azure.Account.Name}** to the Azure Account. 
- Please bind the Resource Group to **#{Azure.ResourceGroup.Name}**
- Leave the deployment mode to Incremental
- Within the Template Source section click on **Add Source Code**
- Paste in the following code: 

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "metadata": {
    "_generator": {
      "name": "bicep",
      "version": "0.14.46.61228",
      "templateHash": "8390431054344291899"
    }
  },
  "parameters": {
    "appname": {
      "type": "string"
    },
    "location": {
      "type": "string",
      "defaultValue": "[resourceGroup().location]"
    },
    "skucode": {
      "type": "string"
    },
    "osType": {
      "type": "string",
      "allowedValues": [
        "windows"
      ]
    }
  },
  "resources": [
    {
      "type": "Microsoft.Web/serverfarms",
      "apiVersion": "2021-03-01",
      "name": "[parameters('appname')]",
      "location": "[parameters('location')]",
      "kind": "",
      "tags": {},
      "properties": {
        "reserved": false
      },
      "sku": {
        "name": "[parameters('skucode')]"
      }
    }
  ]
}
```
- You will now need to populate the parameters
- Appname = #{Azure.appname}
- Locaton = #{Azure.Location.Name}
- SkuCode = #{Azure.skucode}
- osType = Select Windows from the drop down

- Now click on **Save**

### Create a Web App

In this step, we create the [Azure Web App](https://docs.microsoft.com/azure/app-service/)

- In the Runbook, go to **Process** and select **Add Step** and search for **Deploy an Azure Resource Manager template** 
- Name this step **Deploy Azure Web App**
- Set the execution location to **Run once on a worker**
- Ensure the **Default worker pool** is selected
- Ensure **User Azure Tools pre-installed on the worker** is selected
- Please bind **#{Azure.Account.Name}** to the Azure Account. 
- Please bind the Resource Group to **#{Azure.ResourceGroup.Name}**
- Leave the deployment mode to Incremental
- Within the Template Source section click on **Add Source Code**
- Paste in the following code: 

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "metadata": {
    "_generator": {
      "name": "bicep",
      "version": "0.14.46.61228",
      "templateHash": "16552574119515470574"
    }
  },
  "parameters": {
    "webSiteName": {
      "type": "string"
    },
    "location": {
      "type": "string",
      "defaultValue": "[resourceGroup().location]"
    },
    "planName": {
      "type": "string"
    }
  },
  "resources": [
    {
      "type": "Microsoft.Web/sites",
      "apiVersion": "2021-03-01",
      "name": "[parameters('webSiteName')]",
      "location": "[parameters('location')]",
      "properties": {
        "serverFarmId": "[parameters('planName')]",
        "siteConfig": {
          "windowsFxVersion": "dotnetcore|6.0",
          "alwaysOn": true
        }
      }
    }
  ]
}
```

- You will now need to populate the parameters
- WebSiteName = #{Azure.websiteName}
- Locaton = #{Azure.Location.Name}
- PlanName = #{Azure.appname}
- Now click on **Save**

### Register the Web App

In this step, we register the Web App with Octopus Deploy. As we're creating the Infrastructure using Octopus, we also need to register it so we can deploy to it. 

- In the Runbook, go to **Process**, select **Add step** and search for **Run a Script** 
- Call this step  **Register Web App**
- Set the execution location to **Run once on a worker**
- Ensure the worker pool is set to **Default Worker Pool**
- Ensure the script source is set to **inline source code** and **PowerShell**
- Paste the following script into the dialogue box:

```powershell
# Force use of TLS 1.2
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12

# Define parameters
$baseUrl = $OctopusParameters['Global.Base.Url']
$apiKey = $OctopusParameters['Global.Api.Key']
$spaceId = $OctopusParameters['Octopus.Space.Id']
$spaceName = $OctopusParameters['Octopus.Space.Name']
$environmentName = $OctopusParameters['Octopus.Environment.Name']
$environmentId = $OctopusParameters['Octopus.Environment.Id']
$azureAccount = $OctopusParameters['Azure.Account.Name']
$name = $OctopusParameters['Azure.websiteName']
$resourceGroupName = $OctopusParameters['Azure.ResourceGroup.Name']

# Get default machine policy
$machinePolicy = (Invoke-RestMethod -Method Get -Uri "$baseUrl/api/$spaceId/machinepolicies/all" -Headers @{"X-Octopus-ApiKey"="$apiKey"}) | Where-Object {$_.Name -eq "Default Machine Policy"}

# Build JSON payload
$jsonPayload = @{
	Id = $null
    MachinePolicyId = $machinePolicy.Id
    Name = $name
    IsDisabled = $false
    HealthStatus = "Unknown"
    HasLatestCalamari = $true
    StatusSummary = $null
    IsInProcess = $true
    EndPoint = @{
    	Id = $null
        CommunicationStyle = "AzureWebApp"
        Links = $null
        AccountId = $azureAccount
        ResourceGroupName = $resourceGroupName
        WebAppName = $name
    }
    Links = $null
    TenantedDeploymentParticipation = "Untenanted"
    Roles = @(
    	"RandomQuotes-Web"
    )
    EnvironmentIds = @(
    	$environmentId
    )
    TenantIds = @()
    TenantTags = @()
}

# Register the target to Octopus Deploy
Invoke-RestMethod -Method Post -Uri "$baseUrl/api/$spaceId/machines" -Headers @{"X-Octopus-ApiKey"="$apiKey"} -Body ($jsonPayload | ConvertTo-Json -Depth 10)

```

- Now click on **Save**

Our create infrastructure runbook is now complete.  Click on **Run** to start the creation of the infrastructure.  Select **Production** as the environment and click on **Run**. 

The runbook will now work away at creating and registering our infrastructure. 

We are going to move on to create a workbook that will destroying the infrastructure for us. 



## Destroying Infrastructure

In this section, we'll go through the configuration of destroying all your Infrastructure using Octopus Runbooks. 

### De-register the Azure Web App

In this step, we de-register the Web App from Octopus Deploy.

- Browse your RandomQuotes project
- Select **Runbooks** under **Operations**
- Select **Add Runbook**
- Input the name of **Destroy Infrastructure** and select **Save**
- Click on **Define your runbook process**
- Click on **Add Step**
- Search for **Run a Script**
- Name this step **De-register Web App**
- Set the execution location to **Run once on a worker**
- Ensure the worker pool is set to **Default Worker Pool**
- Ensure the script source is set to **inline source code** and **PowerShell**
- Paste the following script into the dialogue box:

```powershell
# Set secure protocols
[System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor [Net.SecurityProtocolType]::Tls11 -bor [System.Net.SecurityProtocolType]::Tls12

$spaceId = $OctopusParameters['Octopus.Space.Id']

# Get machine name
$targetName = $OctopusParameters["Project.WebApp.Name"]

# Get all machines
$deploymentTargets = (Invoke-RestMethod -Method Get -Uri "$($OctopusParameters['Global.Base.Url'])api/$spaceID/machines/all" -Headers @{"X-Octopus-ApiKey"="$($OctopusParameters['Global.Api.Key'])"}) | Where-Object {$_.Name -like "$targetName*"} 

# Loop through returned machines
foreach($deploymentTarget in $deploymentTargets)
{
    # Display what's being removed
    Write-Output "Removing $($deploymentTarget.Name)"
    
    # Remove the machine
    Invoke-RestMethod -Method Delete -Uri "$($OctopusParameters['Global.Base.Url'])api/$spaceID/machines/$($deploymentTarget.Id)" -Headers @{"X-Octopus-ApiKey"="$($OctopusParameters['Global.Api.Key'])"}
}
```
- Click on Save

- Click on **Add Step**
- Search for **Run an Azure Script**
- Call this step **Destroy Resource Group**
- Set the execution location to **Run once on a worker**
- Ensure the worker pool is set to **Default Worker Pool**
- Ensure **User Azure tools bundled with Octopus** is selected within the **Azure Tools** section
- Bind **#{Azure.Account.Name}** in the Azure Account section
- Ensure **inline source code** is selected and **PowerShell**
- Paste the following code into the inline source code: 

```powershell
$resourceGroup = $OctopusParameters["Azure.ResourceGroup.Name"]

$groupExists = az group exists --name $resourceGroup
if($groupExists -eq $true) {
	Write-Host "Deleting Resource Group: $resourceGroup"
    az group delete --name $resourceGroup --yes 
	Write-Highlight "Deleted Resource Group: $resourceGroup"
}
else {
	Write-Highlight "Resource Group: $resourceGroup doesnt exist."
}
```
- Now click on **Save**

## Check Point

You should now have: 

- GitHub Secrets configued to connect to your Octopus Instance
- An Azure Service Principal account setup and connected to your Octopus Deploy environment
- Two runbooks set up within Octopus Deploy for your infrastructure
- A GitHub Action workflow configured and successfully ran
- Your infrastructure should now be deploying or deployed

## Next Section

[Set up the Octopus Deploy Deployment Process](15_Octopus_Deployment.md)