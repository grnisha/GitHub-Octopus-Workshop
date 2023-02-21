#  Azure Infrastructure

## RandomQuotes Background

We will be using the RandomQuotes application in this workshop.  This is a sample application that has been built by the team at Octopus Deploy. 

The sample app is written in .NET Core. 

The solution consists of:
 - Azure Web App
 - Azure Web App Service Plan

## Infrastructure Overview

As a summary, we will deploy:

* 3 x Azure Web Apps (1 for Website, 1 for Product Service, and 1 for the Shopping Cart Service).
* 1 x Azure SQL Server
* 1 x Azure SQL Database

## Azure Bicep Templates

We will be using Azure Bicep templates and [Octopus Runbooks](https://github.com/TechielassInc/GitHub-Octopus-Workshop/blob/main/Workshop/WorkshopGuide/14_terminology.md#what-is-octopus-runbooks) to deploy the infrastructure. 

## Next Section

[Azure_Service_Principals](07_Azure_Service_Principal.md)