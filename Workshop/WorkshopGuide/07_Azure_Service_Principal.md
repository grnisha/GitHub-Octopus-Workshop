# Azure Service Principal Setup

Azure Service Principal accounts are for use with the **Azure Resource Management (ARM) API** only. Configuring your Octopus Server to authenticate with the service principal you create in Azure Active Directory will let you configure finely grained authorization for your Octopus Server.

1. Create an Azure Active Directory registered application (or application registration) and service principal (via the [Azure Portal](#create-service-principal-account-in-azure) or with [PowerShell](#create-service-principal-account-with-powershell)).
2. Allow Octopus to authenticate with Azure using a Service Principal.

## Create an Azure Service Principal within the Azure Shell (PowerShell) {#create-service-principal-account-in-azure}

- Head over to [https://shell.azure.com](https://shell.azure.com)
- Ensure you are within a PowerShell session
- Enter the following command to create an Azure Service Principal:

```powershell
$SPName="give your Service Principal a name"
$subscriptionID="enter your Azure Subscription ID"

az ad sp create-for-rbac --name $SpName --role="Contributor" --scopes="/subscriptions/$subscriptionID" --query "password" -o tsv
```

This will create an Azure Service Principal with contributor access to your subscription.  When the command executes it will output the password of your Service Principal, **take a note of this**, you are going to need this in the next step. 

-  Next within your Shell session enter the following command:

```powershell
(Get-AzureADServicePrincipal -SearchString "$SPName").AppId
```

This retrieves the Application ID for your Service Principal account, **take a note of this**, you are going to need this in the next step. 

- Next within your Shell session enter the following command: 

```powershell
(Get-AzContext).Tenant.id  
```

This retrieves the Tenant ID for your subscription, **take a note of this**, you are going to need this in the next step. 


You now have the following:

- **Tenant ID**
- **Application ID**
- **Application Password/secret**


Now, you can [add the Service Principal Account in Octopus](#add-service-principal-account). 

## Add the Service Principal account in Octopus

Now that you have the following values, you can add your account to Octopus:

- Application ID
- Tenant ID
- Application Password/Key

1. Navigate to **{{Infrastructure,Account}}**.
1. Select **{{ADD ACCOUNT,Azure Subscriptions}}**.
1. Give the account the name you want it to be known by in Octopus.
1. Give the account a description.
1. Add your Azure Subscription ID. This is found in the Azure portal under **Subscriptions**.
1. Add the **Application ID**, the **Tenant ID**, and the **Application Password/Keyword**.

Click **SAVE AND TEST** to confirm the account can interact with Azure. Octopus will then attempt to use the account credentials to access the Azure Resource Management (ARM) API and list the Resource Groups in that subscription. 

A newly created Service Principal may take several minutes before the credential test passes. If you have double checked your credential values, wait 15 minutes and try again.

Octopus Deploy now has access to be able to deploy, delete, modify resources inside your Azure subscription. 

## Azure account variables

You can access your Azure account from within projects through a variable of type **Azure Account**. Learn more about [Azure Account Variables](https://octopus.com/docs/projects/variables/azure-account-variables.md) and [Azure Deployments](https://octopus.com/docs/deployments/azure/index.md).

[Return to workshop steps](01_Summary.md#agenda)