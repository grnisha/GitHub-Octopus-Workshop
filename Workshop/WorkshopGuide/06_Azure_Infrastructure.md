#  Azure Infrastructure

## RandomQuotes Background

We will be using the RandomQuotes application in this workshop.  This is a sample application that has been built by the team at Octopus Deploy. 

The sample app is written in .NET Core. 

The solution consists of:
 - Azure Web App
 - Azure Web App Service Plan

It is a simple application, but it can be used to show off a few features within Octopus Deploy. 

## Azure ARM Templates

We will be using Azure ARM templates and [Octopus Runbooks](https://github.com/TechielassInc/GitHub-Octopus-Workshop/blob/main/Workshop/WorkshopGuide/15_terminology.md#what-is-octopus-runbooks) to deploy the infrastructure. 

Octopus Deploy natively supports deploying ARM Templates.  It can deploy Azure Bicep templates, but it is a more complex process. 

## Next Section

[Azure_Service_Principals](07_Azure_Service_Principal.md)