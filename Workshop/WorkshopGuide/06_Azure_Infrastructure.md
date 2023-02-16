# NDCDevOpsWorkshop Azure Infrastructure

This section will be instructor-led, but full details should be below.

## OctoPetShop Background

[OctoPetShop](https://github.com/OctopusDeployCommunity/NDCDevOpsWorkshop) is a sample application built to demonstrate a multi-tier application deployed using Octopus Deploy.

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

## What are ARM Templates

An Azure Resource Manager(ARM) template is a JavaScript Object Notation (JSON) file that defines the infrastructure and configuration for your project.

Many teams have adopted agile development methods, with more companies moving to the cloud. These teams iterate quickly. They need to deploy their solutions to the cloud repeatedly and know their infrastructure is reliable. As infrastructure has become part of the iterative process, the division between operations and development has disappeared. Teams need to manage infrastructure and application code through a unified approach.

To meet these challenges, you can automate deployments and adopt the practice of infrastructure as code.

In code, you define the infrastructure that needs to be deployed. The infrastructure code becomes part of your project. Like the application code, you store the infrastructure code in a source repository and version it, and anyone on your team can run the code and deploy similar environments.

Use Azure Resource Manager templates to implement infrastructure as code for your Azure solutions.

The template is a JavaScript Object Notation (JSON) file that defines the infrastructure and configuration for your project. The template uses declarative syntax, which lets you state what you intend to deploy without writing the sequence of programming commands to create it.

In the template, you specify the resources to deploy and the properties for those resources.

You can deploy software to the Azure cloud by adding your Azure subscription to Octopus. With an active Azure subscription, you can use Octopus to deploy to [Azure Web App](https://octopus.com/docs/infrastructure/deployment-targets/azure/web-app-targets/index.md) targets.

Before deploying Infrastructure to Azure, you need to add your Azure subscription to Octopus Deploy.

## Next Section

[Azure_Service_Principals](07_Azure_Service_Principal.md)