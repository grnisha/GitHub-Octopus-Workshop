#  Octopus Runbook Configuration

[Octopus Deploy Runbooks](https://octopus.com/docs/runbooks) is a way to automate routine maintenance and emergency operations tasks, such as infrastructure provisioning, database management, and website failover and restoration.

In this section, we'll detail how to set up your Infrastructure using Infrastructure as Code, and we'll provision all resources automatically using Octopus Runbooks. 

No infrastructure should be set up manually. 

## Creating Infrastructure

In this section, we'll go through the configuration of spinning up all your Infrastructure as Code using Octopus Runbooks. Please ensure you have the [repo](https://github.com/OctopusDeployCommunity//tree/main/Workshop/ARM/Create_Infrastructure) open. We're using ten steps, and most of the scripts and ARM Templates are located in this repository to avoid having to list them in the guide.

You can see an example of this [here](https://webinar.octopus.app/app#/Spaces-142/projects/octopetshop/operations/runbooks/Runbooks-923/process/RunbookProcess-Runbooks-923).

Please use **Use Azure tools bundled with Octopus for custom scripts** option on all steps.

### Creating Resource Group

In this step, we create the [Azure Resource Group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal). 

- Browse your OctoPetShop project
- Select **Runbooks** under **Operations**
- Select **Add Runbook**
- Input the name of **Create Infrastructure** and select **Save**
- Go to **Process** and select **Add Step** and select **Run an Azure Script** and name **Create Resource Group**
- Please bind **#{Azure.Account.Name}** to the Azure Account. 
- Paste the script from the repository and ensure **PowerShell** is selected

### Deploy Azure SQL Server

In this step, we create the [Azure SQL Server](https://docs.microsoft.com/en-us/azure/azure-sql/database/sql-database-paas-overview?view=azuresql)

- In the Runbook, go to **Process** and select **Add Step** and select **Deploy an Azure Resource Manager template** and name **Deploy Azure SQL Server**
- Please bind **#{Azure.Account.Name}** to the Azure Account. 
- Paste the ARM Template in from the repository
- You will need to set up the Parameters now using Variables or inputs
- administratorLogin = #{Project.Database.Admin.Username}
- administratorLoginPassword = #{Project.Database.Admin.Password}
- location = #{Azure.Location.Name}
- serverName = #{Project.Database.Server}
- enableADS = false
- useVAManagedIdentity = false
- allowAzureIPs = true
- enableVA = false
- serverTags = {}

### Deploy Empty Database

In this step, we create the [Azure SQL Server Database](https://docs.microsoft.com/en-us/azure/azure-sql/database/sql-database-paas-overview?view=azuresql)

- In the Runbook, go to **Process** and select **Add Step** and select **Deploy an Azure Resource Manager template** and name **Deploy Empty Database**
- Please bind **#{Azure.Account.Name}** to the Azure Account. 
- Paste the ARM Template in from the repository
- You will need to set up the Parameters now using Variables or inputs
- serverName = #{Project.Database.Server}
- sqlDBName = #{Project.Database.Name}
- location = #{Project.Database.Location}
- administratorLogin = #{Project.Database.Admin.Username}
- administratorLoginPassword = #{Project.Database.Admin.Password}

### Create App Service Plan

In this step, we create the [Azure App Service Plan](https://docs.microsoft.com/en-us/azure/app-service/)

- In the Runbook, go to **Process** and select **Add Step** and select **Deploy an Azure Resource Manager template** and name **Create App Service Plan**
- Please bind **#{Azure.Account.Name}** to the Azure Account. 
- Paste the ARM Template in from the repository
- You will need to set up the Parameters now using Variables or inputs
- name = #{Azure.WebApp.HostingPlan.Name}
- location = #{Azure.Location.Abbr}
- sku = #{Azure.WebApp.Sku}
- skucode = #{Azure.WebApp.Sku.Code}
- osType = #{Project.AzureAppServicePlan.Type}

### Create Product Service Web App

In this step, we create the [Azure Web App](https://docs.microsoft.com/en-us/azure/app-service/)

- In the Runbook, go to **Process** and select **Add Step** and select **Deploy an Azure Resource Manager template** and name **Create ProductService Web App**
- Please bind **#{Azure.Account.Name}** to the Azure Account. 
- Paste the ARM Template in from the repository
- You will need to set up the Parameters now using Variables or inputs
- name = #{Project.ProductService.Name}
- location = #{Azure.Location.Abbr}
- hostingPlanName = #{Azure.WebApp.HostingPlan.Name}
- serverFarmResourceGroup = #{Azure.ResourceGroup.Name}
- alwaysOn = False
- currentStack = #{Azure.WebApp.Stack.Name}
- phpVersion = #{Azure.WebApp.Php.Version}
- errorLink = #{Azure.WebApp.ErrorLink}

### Register Product Service Web App

In this step, we register the Web App with Octopus Deploy. As we're creating the Infrastructure using Octopus, we also need to register it so we can deploy it. 

- In the Runbook, go to **Process**, select **Add step** and select **Run a Script** and name **Register ProductService Web App**
- Paste the script from the repository and ensure **PowerShell** is selected

### Create Shopping Cart Service Web App

In this step, we create the [Azure Web App](https://docs.microsoft.com/en-us/azure/app-service/)

- In the Runbook, go to **Process** and select **Add Step** and select **Deploy an Azure Resource Manager template** and name **Create Resource Group**
- Please bind **#{Azure.Account.Name}** to the Azure Account. 
- Paste the ARM Template in from the repository.
- You will need to set up the Parameters now using Variables or inputs
- name = #{Project.ShoppingCartService.Name}
- location = #{Azure.Location.Abbr}
- hostingPlanName = #{Azure.WebApp.HostingPlan.Name}
- serverFarmResourceGroup = #{Azure.ResourceGroup.Name}
- alwaysOn = False
- currentStack = #{Azure.WebApp.Stack.Name}
- phpVersion = #{Azure.WebApp.Php.Version}
- errorLink = #{Azure.WebApp.ErrorLink}

### Register Shopping Cart Service Web App

In this step, we register the Web App with Octopus Deploy. As we're creating the Infrastructure using Octopus, we also need to register it so we can deploy it. 

- In the Runbook, go to **Process**, select **Add step** and select **Run a Script** and name **Register Shopping Cart Web App**
- Paste the script from the repository and ensure **PowerShell** is selected.

### Create OctoPetShop Website Web App

In this step, we create the [Azure Web App](https://docs.microsoft.com/en-us/azure/app-service/)

- In the Runbook, go to **Process** and select **Add Step** and select **Deploy an Azure Resource Manager template** and name **Create Resource Group**
- Please bind **#{Azure.Account.Name}** to the Azure Account. 
- Paste the ARM Template in from the repository
- You will need to set up the Parameters now using Variables or inputs
- name = #{Project.WebApp.Name}
- location = #{Azure.Location.Abbr}
- hostingPlanName = #{Azure.WebApp.HostingPlan.Name}
- serverFarmResourceGroup = #{Azure.ResourceGroup.Name}
- alwaysOn = False
- currentStack = #{Azure.WebApp.Stack.Name}
- phpVersion = #{Azure.WebApp.Php.Version}
- errorLink = #{Azure.WebApp.ErrorLink}

### Register Website App

In this step, we register the Web App with Octopus Deploy. As we're creating the Infrastructure using Octopus, we also need to register it to deploy it. 

- In the Runbook, go to **Process**, select **Add step** and select **Run a Script** and name **Register OctoPetShop Web App**
- Paste the script from the repository and ensure **PowerShell** is selected

## Destroying Infrastructure

In this section, we'll go through the configuration of destroying all your Infrastructure using Octopus Runbooks. Please ensure you have the [repo](https://github.com/OctopusDeployCommunity//tree/main/Workshop/ARM/Destroy_Infrastructure) open. There are four steps we're using scripts only. Please use the scripts in the repository to avoid listing them out here.

We recommend that if you use Infrastructure as Code to tear it down, then use IaC to also allow for easy spinning up and tearing down of resources.

You can see an example of this [here](https://webinar.octopus.app/app#/Spaces-142/projects/octopetshop/operations/runbooks/Runbooks-924/process/RunbookProcess-Runbooks-924).

Please use **Use Azure tools bundled with Octopus for custom scripts** option on all steps.

### De-register ProductService Web App

In this step, we de-register the Web App from Octopus Deploy.

- Browse your OctoPetShop project
- Select **Runbooks** under **Operations**
- Select **Add Runbook**
- Input the name of **Destroy Infrastructure** and select **Save**
- In the Runbook, go to **Process** and select **Add step** and select **Run a Script** and name **De-register ProductService Web App**
- Input PowerShell script that will de-register. Please ensure you use the correct PowerShell script.
- All other options should remain on default values.

### De-register ShoppingCart Service Web App

In this step, we de-register the Web App from Octopus Deploy.

- In the Runbook, go to **Process** and select **Add step** and select **Run a Script** and name **De-register ShoppingCart Service App**
- Input PowerShell script that will de-register. Please ensure you use the correct PowerShell script.
- All other options should remain on default values.

### De-register Web App

In this step, we de-register the Web App from Octopus Deploy.

- In the Runbook, go to **Process** and select **Add step** and select **Run a Script** and name **De-register Web Web App**
- Input PowerShell script that will de-register. Please ensure you use the correct PowerShell script.
- All other options should remain on default values.

### Destroying Resource Group

In this step, we destroy the [Azure Resource Group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal), which tears down all of our Infrastructure. 

- Go to **Process** and select **Add Step** and select **Run an Azure Script** and name **Destroy Resource Group**
- Please bind **#{Azure.Account.Name}** to the Azure Account. 
- Paste the script from the repository and ensure **PowerShell** is selected
- Select Save

## Wrap-up

At the end of this section, you have completed the fundamentals of the Workshop. 

You should now have: 

- A Github Action configured and ready to be run in your local organization
- Github Secrets configured to connect to your Octopus instance from the SVC-GHA account, which is embedded in the Build Server Team and should have permissions to create and run deployments. 
- A fully active Azure Service Principal account that has been configured in Octopus to all environments. This should be configured in the Octopus UI, and the test should have passed successfully.
- A Octopus Infrastructure service account can register deployment targets via the Octopus API. This account should be embedded in the Infrastructure Team. 
- A fully configured OctoPetshop Deployment process.
- A fully configured Runbook that provisions all of the Infrastructure using IaC and a Runbook that will tear it all down.

## Next Section

[Execution Instruction](11_Execution.md)