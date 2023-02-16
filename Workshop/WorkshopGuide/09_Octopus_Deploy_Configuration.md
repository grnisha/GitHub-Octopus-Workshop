# NDCDevOpsWorkshop Octopus Configuration

## Octopus Configuration

The Octopus Deployment configuration will be done using class-led instructions, but you can follow along below if you have completed previous tasks or need a refresher.

## Adding Environments

Since environments are the phases you move your code through, they form the backbone of your deployment pipeline. Before you configure anything else, you should configure your environments.

The most common setup is four environments. These are:

1. **Development** or **Dev** for short, is for developers to experiment on. It's generally in flux and can often be expected to be unavailable.
1. **Test/QA** - Quality assurance teams test functionality in the test environment.
1. **Staging/Pre-Production** - Staging is used as a final sanity check before deploying to Production.
1. **Production** is where your end users usually use your software outside testing.

However, we didn't design Octopus Deploy to force people to use a set of predefined environments. Some companies only have three environments. Others have many more. Likewise, not everyone names their environments the same way. One person's Test is another person's QA. It's essential that you can call your environments in the way that best supports your organization's needs.

### Adding your environment

In our example, we will configure a single environment of **Production** so we can focus on learning about DevOps and broader concepts. 

- Logon to your Octopus instance
- Browse to Infrastructure -> Environments
- Select **Add environment**
- A small window should pop up. Input **Production** for the name. 
- Please ensure **Dynamic Infrastructure** is set yes. 

## Projects

Projects let you create and manage your deployment processes, releases, and runbooks from the Octopus REST API and Octopus Web Portal.

For each project, you can define a deployment process, runbooks to manage your Infrastructure, variables, the environments where the software will be deployed, and releases of your software.

You can manage your projects by navigating to the Projects tab in the Octopus Web Portal:

## Add a project

Before you can define your deployment processes or runbooks, you must create a project:

1. Select **Projects** from the main navigation and click **ADD PROJECT**.
1. Name it **OctoPetShop-YourInitials**. So, if your initials are DC, it should be called **OctoPetShop-DC**. This is needed as we'll create Infrastructure using Runbooks using Octopus Variables. **Do not use the option for Version Control for this project as we'll enable this later as part of the Config as Code topic.**

Now that you've created a project, you can define your [deployment process](https://octopus.com/docs/projects/deployment-process/index.md) or [runbooks](https://octopus.com/docs/runbooks/index.md).

## Project settings

You can change the project's settings by accessing the main page's settings menu. The settings you can change are:

- Name.
- Enable or disable the project to allow or prevent releases and deployments from being created.
- [Logo](#project-logo)
- Description
- [Project Group](#project-group)
- [Release Versioning](/docs/releases/release-versioning.md)
- [Release Notes Template](/docs/releases/release-notes.md#Release-Notes-Templates)

### Deployment settings

- Package re-deployment
    - Specify always to deploy all packages or skip any package steps already installed.
- Deployment targets
    - Specify if deployments are allowed if there are no deployment targets:
        - Deployments with no target are allowed - There must be at least one enabled healthy target to deploy to in the environment.
        - Allow deployments to be created when there are no deployment targets - Use this where no steps in the process have targets (or are all run on the Server), or you are dynamically adding targets during deployment.
- Deployment target status
    - Choose to skip unavailable or exclude unhealthy targets from the deployment.
- [Deployment changes template](docs/releases/deployment-notes.md#Templates)
    - Specify a template for each deployment's changes.
- Default failure mode
    - Specify whether or not to use [guided failure mode](/docs/releases/guided-failures.md).

## Project logo {#project-logo}

Customize your project logo to make it easily identifiable amongst other projects.

1. From the project's main page, select **Settings**.
2. Click the **Logo** section of the settings page.
3. Select from our built-in icon library paired with your choice of color or upload a custom image.
4. Click **Save**.

For custom images, in addition to supporting .jpg and .png files, we also support .gif files. This means you can have an animated icon to add a little flair to your Octopus Deploy instance!

## Adding your laptop as a deployment target

In this section, I'll take you through how to use your laptop as a worker. We'll use this as a way to deploy your database, and you could also use it as a deployment target for Development, but this is out of scope for this part. If you cannot install the Tentacle, please speak to the workshop leader as they can provide a deployment target on your behalf.

- Browse to https://octopus.com/downloads
- Select Tentacle and download it
- Run the Windows installer locally and set it up as a [Polling Tentacle](https://octopus.com/docs/infrastructure/deployment-targets/windows-targets#configure-a-polling-tentacle) and register it to your cloud instance with the below values: 
- Name: **Bastion**
- Environments: **Production**
- Target Roles: **Bastion**

## Variable Setup

### Global Variable Set Setup

[Library Variable Sets](https://octopus.com/docs/projects/variables/library-variable-sets) is a way for you to define variables across multiple projects. In our example, we're going to define a **Global Variable Set** to be used for all Projects inside of Octopus.

- Browse to Library-> Variable Sets
- Create a Variable Set named **Global**
- Create a Variable called **Global.API.Key** and use a freshly generated [API key](https://octopus.com/docs/octopus-rest-api/how-to-create-an-api-key) with Space Manager permissions.
- Create a Variable called **Global.Base.URL** and use the URL of your Octopus instance. If you created one name **ndcworkshopexample. Octopus.app** then this is what you'd input. 
- Create a Variable called **Global.Environment.Prefix** and input **p** and scope it to the Production environment.
- Create a Variable called **Global.Environment.Suffix** and input **prod** and scope it to the Production environment.
- Create a Variable called **Global.Server.Thumbprint** and input your Octopus Server Thumbprint. You can get this from Octopus->Configuration->Thumbprint

### Azure Variable Set setup

In this section, we will now define the Azure Variable Set, which can be used by all of your Projects, as we're only defining a single Project that could easily be used in the Project variables, but let's set ourselves up for success and scalability!

We're deliberately going to leave one Variable out for the time being, and we'll come back to that later after we have set up Azure.

- Browse to Library-> Variable Sets
- Create a Variable Set named **Azure**
- Create a Variable called **Azure.Location.Abbr** and input **australiaeast**
- Create a Variable called **Azure.Location.Name** input **Australia East**
- Create a Variable called **Azure.ResourceGroup.Name** and input **#{Octopus.Space.Name | ToLower | Replace " "}-#{Octopus.Project.Name | ToLower | Replace " "}-#{Octopus.Environment.Name | ToLower}-rg**.
- Create a Variable called **Azure.SQL.Server.Admin.Password** and input **A secure password you would use for an Azure SQL Server** and scope it to the Production environment.
- Create a Variable called **Azure.SQL.Server.Admin.Username** and input **A username you would use for an Azure SQL Server** and scope it to the Production environment. Please don't use "admin", "superuser" as these are not allowed. Consider using your full name. 
- Create a Variable called **Azure.SQL.Server.FQDN** and input **#{Azure.SQL.Server.Name}.database.windows.net**
- Create a Variable called **Azure.SQL.Server.Name** input **#{Octopus.Space.Name | ToLower | Replace " "}-#{Octopus.Project.Name | ToLower | Replace " "}-#{Octopus.Environment.Name | ToLower | Replace " "}**
- Create a Variable called **Azure.SQL.Server.Sku** and input **Basic**
- Create a Variable called **Azure.SQL.Server.Tier** input **Basic**
- Create a Variable called **Azure.WebApp.HostingPlan.Name** and input **#{Octopus.Space.Name | ToLower | Replace " "}-#{Octopus.Project.Name | Replace " "}-#{Octopus.Environment.Name | Replace " "}**
- Create a Variable called **Azure.WebApp.Php.Version** input **OFF**
- Create a Variable called **Azure.WebApp.Sku** and input **Standard**
- Create a Variable called **Azure.WebApp.Sku.Code** input **S1**
- Create a Variable called **Azure.WebApp.Stack.Name** input **dotnetcore**

### Project Variables

In this section, we will now define the [Project Variables](https://octopus.com/docs/projects/variables). We are mixing Project and Library Variable sets as this is more real world. Still, these variables could be either in the Library Variable Set or as Project Variables.

- Browse to your OctoPetshop project -> Variables -> Variables
- Create a Variable called **#{Global.Environment.Abbr}_OctoPetShop** and input **2.1.13**
- Create a Variable called **AppSettings:AppVersion** input **#{Octopus.Release.Number}**
- Create a Variable called **AppSettings:ProductServiceBaseUrl** and input **https://#{Project.ProductService.Name}.azurewebsites.net/**
- Create a Variable called **AppSettings:ShoppingCartServiceBaseUrl** input **https://#{Project.ShoppingCartService.Name}.azurewebsites.net/**
- Create a Variable called **ConnectionStrings:OPSConnectionString** and input **Server=#{Project.Database.Server.FQDN};Database=#{Project.Database.Name}; User ID=#{Project.Database.Admin.Username}; Password=#{Project.Database.Admin.Password}**
- Create a Variable called **Project.AzureAppServicePlan.Type** input **windows**
- Create a Variable called **Project.Database.Admin.Password** input **A Secure password of your choosing** and map it to **Production**
- Create a Variable called **Project.Database.Admin.Username** and input **a non-default username** and map it to Production
- Create a Variable called **Project.Database.ConnectionString** and input **#{ConnectionStrings:OPSConnectionString}**
- Create a Variable called **Project.Database.Location** and input **australiaeast**
- Create a Variable called **Project.Database.Name** and input **OctoPetShop**
- Create a Variable called **Project.Database.Server** and input **#{Azure.SQL.Server.Name}**
- Create a Variable called **Project.Database.Server.FQDN** and input **#{Azure.SQL.Server.FQDN}**
- Create a Variable called **Project.Database.Sku** and input **#{Azure.SQL.Server.Sku}**
- Create a Variable called **Project.Database.Tier** and input **#{Azure.SQL.Server.Tier}**
- Create a Variable called **Project.Dotnet.Version** and input **2.1.13**
- Create a Variable called **Project.ProductService.Name** and input **#{Octopus.Environment.Name | ToLower | Replace " "}-#{Octopus.Space.Name | ToLower | Replace " "}-#{Octopus.Project.Name | ToLower | Replace " "}-productservice**
- Create a Variable called **Project.ShoppingCartService.Name** and input **#{Octopus.Environment.Name | ToLower | Replace " "}-#{Octopus.Space.Name | ToLower | Replace " "}-#{Octopus.Project.Name | ToLower | Replace " "}-shoppingcartservice**
- Create a Variable called **Project.Web.URL** and input **https://#{Octopus.Environment.Name}-#{Octopus.Space.Name | ToLower | Replace " "}-#{Octopus.Project.Name}-web.azurewebsites.net**
- Create a Variable called **Project.WebApp.Name** and input **#{Octopus.Environment.Name | ToLower | Replace " "}-#{Octopus.Space.Name | ToLower | Replace " "}-#{Octopus.Project.Name | ToLower | Replace " "}-web**

### Add Library Variable Sets to your project

- Browse your project
- Under **Variables** please select **Library Set**
- Select the button called **Include Library Variable Sets**
- Select both your **Global** and **Azure** Library Variable Sets
- You can now use the Variables in the Variable Set as part of your projects. Without this, you would only have access to the Project Variables

## Octopus Deployment process

In this section, we will define the deployment process for the OctoPetShop project. 

### Azure Website Web App Steps

- Browse your OctoPetShop Project
- Select **Process** under **Deployments**
- Select **Add Step** and select the **Deploy an Azure Web App (Web Deploy)** step
- In the newly created step, add a name of **Deploy Azure OctoPetShop Web**
- Ensure it runs from a Worker on behalf of **OctoPetShop-Web**
- Ensure the step is using **Use Azure tools bundled with Octopus for custom scripts**
- Please ensure you use the built-in Package repository and specify the package name of **OctopusSamples.OctoPetShop.Web**
- Leave all options under the **Deployment** section to remain at default. 
- Under **Structured Configuration Variables** input **appsettings.json**
- All other options should remain the default values.

### Product Service

- Browse your OctoPetShop Project
- Select **Process** under **Deployments**
- Select **Add Step** and select the **Deploy an Azure Web App (Web Deploy)** step
- In the newly created step, add a name of **Deploy OctoPetShop Product Service Web App**
- Ensure it runs from a Worker on behalf of **OctoPetShop-Product-Service**
- Ensure the step is using **Use Azure tools bundled with Octopus for custom scripts**
- Please ensure you use the built-in Package repository and specify the package name of **OctopusSamples.OctoPetShop.ProductService**
- Leave all options under the **Deployment** section to remain at default. 
- Under **Structured Configuration Variables** input **appsettings.json**
- All other options should remain the default values.

### Shopping Cart Service

- Browse your OctoPetShop Project
- Select **Process** under **Deployments**
- Select **Add Step** and select the **Deploy an Azure Web App (Web Deploy)** step
- In the newly created step, add a name of **Deploy OctoPetShop Shopping Cart Service Web App**
- Ensure it runs from a Worker on behalf of **OctoPetShop-ShoppingCart-Service**
- Ensure the step is using **Use Azure tools bundled with Octopus for custom scripts**
- Please ensure you use the built-in Package repository and specify the package name of **OctopusSamples.OctoPetShop.ShoppingCartService**
- Leave all options under the **Deployment** section to remain at default. 
- Under **Structured Configuration Variables** input **appsettings.json**
- All other options should remain the default values.

### Database

- Browse your OctoPetShop Project
- Select **Process** under **Deployments**
- Select **Add Step** and select the **Deploy a Package** step
- In the newly created step, add a name of **Deploy OctoPetShop Database**
- Ensure it runs on each deployment target with the role specified as **Bastion**
- Please ensure you use the built-in Package repository and specify the package name of **OctopusSamples.OctoPetShop.Database**
- All other options should remain the default values.

Your Octopus Deployment process is now completed.

## Next Section

[Octopus Runbooks](10_Octopus_Runbooks.md)