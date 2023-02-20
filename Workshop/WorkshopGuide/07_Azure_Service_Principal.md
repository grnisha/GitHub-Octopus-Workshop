# Azure Service Principal Setup

Azure Service Principal accounts are for use with the **Azure Resource Management (ARM) API** only. Configuring your Octopus Server to authenticate with the service principal you create in Azure Active Directory will let you configure finely grained authorization for your Octopus Server.

1. Create an Azure Active Directory registered application (or application registration) and service principal (via the [Azure Portal](#create-service-principal-account-in-azure) or with [PowerShell](#create-service-principal-account-with-powershell)).
2. Allow Octopus to authenticate with Azure using a Service Principal.

## Create an Azure Service Principal with the Azure Portal {#create-service-principal-account-in-azure}

This step shows you how to create a Service Principal with the Azure Portal, if you would rather use PowerShell to create the Service Principal, see [Create an Azure Service Principal With PowerShell](#create-service-principal-account-with-powershell).

1. In the Azure Portal, navigate to **{{Azure Active Directory,Properties}}** and copy the value from the **Tenant ID** field, this is your **Tenant ID**.
2. Next you need your **Application ID**.
  - If you have created an AAD registered application, navigate to **{{Azure Active Directory,App Registrations}}**, click **View all applications**, select the app and copy the **Application ID**.  Please note, the Azure UI defaults to **Owned Applications** tab.  Click the **All Applications** tab to view all app registrations. 
  - If you haven't created a registered app, navigate to **{{Azure Active Directory,App Registrations}}**, click on **New registration** and add the details for your app, and click **Save**. Make note of the **Application ID**.
3. Generate a one-time password by navigating to **{{Certificates & Secrets,Certificates & Secrets}}**. Add a new **secret**, enter a description, and click **Save**. Make note of the displayed application password for use in Octopus. If you don’t want to accept the default one year expiry for the password, you can change the expiry date.

You now have the following:

- **Tenant ID**
- **Application ID**
- **Application Password/secret**

Next, you need to configure your [resource permissions](#resource-permissions).

## Resource permissions {#resource-permissions}

The final step is to ensure your registered app has permission to work with your Azure resources.

1. In the Azure Portal navigate to **Resource groups** and select the resource group(s) that you want the registered app to access.
1. Next, select the **Access Control (IAM)** option and if your app isn't listed, click **Add**. Select the appropriate role (**Contributor** is a common option) and search for your new application name. Select it from the search results and then click **Save**.

Now, you can [add the Service Principal Account in Octopus](#add-service-principal-account).

Note on roles: Your Service Principal will need to be assigned the *Contributor* role in order to deploy.

It will also need the *Reader* role on the subscription itself.



Now, you can [add the Service Principal Account in Octopus](#add-service-principal-account). Consider reading our [note on least privilege first](#note_on_lease_privilege).

## Add the Service Principal account in Octopus {#add-service-principal-account}

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

Click **SAVE AND TEST** to confirm the account can interact with Azure. Octopus will then attempt to use the account credentials to access the Azure Resource Management (ARM) API and list the Resource Groups in that subscription. You may need to include the appropriate IP Addresses for the Azure Data Center you are targeting in any firewall allow list. See [deploying to Azure via a Firewall](/docs/deployments/azure/index.md) for more details.

A newly created Service Principal may take several minutes before the credential test passes. If you have double checked your credential values, wait 15 minutes and try again.

## Azure account variables {#azure-account-variables}

You can access your Azure account from within projects through a variable of type **Azure Account**. Learn more about [Azure Account Variables](https://octopus.com/docs/projects/variables/azure-account-variables.md) and [Azure Deployments](https://octopus.com/docs/deployments/azure/index.md).