# Workshop Guide

## Summary

The purpose of this repository is to take you through deploying resources in Azure, using GitHub Actions and Octopus Deploy. 

This workshop has been designed by [Sarah Lean](https://www.linkedin.com/in/sazlean/). 

This workshop has been designed for those that are familiar with Azure and the concepts of DevOps deployments.  You can work through the workshop at your own pace without any assistance. 

## Agenda

During the workshop you will find all the resources that you need within this repository.   You'll walk through building a sample application, testing it in GitHub Actions, configuring it for release and then passing it off to Octopus Deploy for deploment. 

There are 10 steps to completing this workshop, you can work through them at your own pace. 

- Step 1: [Sign up for an Azure Trial](05_Azure_Sign_up.md)
- Step 2: [Sign up for an GitHub Account](03_Github_Sign_up.md)
- Step 3: [Sign up for an Octopus Deploy Trial](04_Octopus_Deploy_Cloud_Sign_up.md)
- Step 4: [Set up an Azure Service Principal](07_Azure_Service_Principal.md)
- Step 5: [Configure your GitHub repository and workflow](08_Github_Actions_Configuration.md)
- Step 6: [Set up your Octopus Deploy project and variables](09_Octopus_Deploy_Initial_Setup.md)
- Step 7: [Configure the Octopus Deploy Runbook to deploy the infrastructure](10_Octopus_Runbooks.md)
- Step 8: [Configure the Octopus Deploy deployment](12_Octopus_Deployment.md)
- Step 9: [Execute a release and deployment](11_Execution.md)
- Step 10: [Add more complexity to your deployment](13_Add_complexity.md)
- Step 11: [Wrap up](14_Wrap_Up.md)


### We'll introduce you to: 

- GitHub and GitHub Actions
- Octopus Cloud
- Microsoft Azure
- Setting up your application to pass packages to Octopus Deploy from GitHub
- Octopus Runbooks
- Infrastructure as Code (IaC) and how to add infrastructure in Octopus Deploy


### Intended Audience:

- Developers, Ops, and DevOps Engineers starting on their CI/CD journey
- Software engineers looking for fresh ideas

### Prerequisites:

- Free Azure or MSDN Subscription with access to create an Azure Service Principal 
- Email address to spin up your free Octopus instance
- GitHub account


## Next Section

[Prerequisites](02_Prerequisites.md)