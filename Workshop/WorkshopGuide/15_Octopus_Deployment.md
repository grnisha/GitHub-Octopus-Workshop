# Octopus Deployment process

In this section, we will define the deployment process for the RandomQuote application.  

### Azure Website Web App Steps

- Browse your Project
- Select **Process** under **Deployments**
- Select **Create Process**
- Search for **Deploy an Azure Web App (Web Deploy)** step
- In the newly created step, add a name of **Deploy Azure RandomQuote Front End Web App**
- Within Worker Pool ensure it is set to **Runs on a worker from a specific worker pool - Default worker pool**
---onbehalfof?
- Ensure the step is using **Use Azure tools bundled with Octopus for custom scripts**
- Please ensure you use the built-in Package repository and specify the package name of **OctopusSamples.OctoPetShop.Web**
- Leave all options under the **Deployment** section to remain at default. 
- Under **Structured Configuration Variables** input **appsettings.json**
- All other options should remain the default values.