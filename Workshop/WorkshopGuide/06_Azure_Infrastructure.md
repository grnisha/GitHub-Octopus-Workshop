#  Azure Infrastructure


## OctoPetShop Background

[OctoPetShop](https://github.com/OctopusDeployCommunity/OctoPetShop) is a sample application built to demonstrate a multi-tier application deployed using Octopus Deploy.  This sample application was built by the Octopus Deploy team. 

Octopus Pet Shop Example Web app written in .NET Core. This solution consists of:
 - Octopus Pet Shop Web App
 - Product Service
 - Shopping Cart Service
 - Database project using Dbup

## Infrastructure Overview

As a summary, we will deploy:

* 3 x Azure Web Apps (1 for Website, 1 for Product Service, and 1 for the Shopping Cart Service).
* 1 x Azure SQL Server
* 1 x Azure SQL Database

## Azure Bicep Templates

We will be using Azure Bicep templates and [Octopus Runbooks](https://github.com/TechielassInc/GitHub-Octopus-Workshop/blob/main/Workshop/WorkshopGuide/14_terminology.md#what-is-octopus-runbooks) to deploy the infrastructure. 

## Next Section

[Azure_Service_Principals](07_Azure_Service_Principal.md)