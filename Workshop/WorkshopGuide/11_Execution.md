# NDCDevOpsWorkshop Execution Instructions

In this section, we will take all your work on Github, Azure, and Octopus and run a complete CI/CD pipeline, create the Infrastructure and deploy the application and database.

This section will be class-led, but this document should contain all details to allow you to work at your own pace. 

## Runbook

In our example, we don't have any infrastructure to deploy to, so we'll need to run the **Create Infrastructure** Runbook to create it. 

- Logon to Octopus
- Browse to your **OctoPetshop** project and select Operations -> Runbooks
- Select **Create Infrastructure** and ensure the Runbook has been published. 
- Select Run, and use **Production**. 
- It should take about 10 minutes for your Infrastructure to be created, but it can sometimes be shorter and more prolonged. 

### Verification

At the end of the Runbook, you should have

- 3 Web Apps - One for the website, one for the Product Service, and one for the Shopping Cart Service
- 1 Azure SQL Server
- 1 Empty Azure SQL Database

We won't add the Azure SQL server or the Database to Octopus as a deployment target, but you can confirm the Web Apps are displayed under **Infrastructure -> Deployment Targets**

## Deployment

Next up, we will build the code and database and pass the artifact to Octopus to allow for deployment. 

- Logon to Github.com/YOURORGANIZATIONNAME/NDCDevOpsWorkshop
- Browse to **Actions**
- Select your GitHub Action and select **Run Workflow**
- It should now run your build, pass your artifact to Octopus and start the deployment to Production for you. 

Please raise any issues you experience with the Workshop leader, and they can troubleshoot with you. 

## Next Section

The Workshop is now completed, but if you're completed ahead of time, please check out the [Additional Information Section](12_Additional_Information.md) as this has a list of topics you can learn if there's enough time.