# NDCDevOpsWorkshop

## Summary

Each part of the workshop is split into separate chapters. We will start by configuring and signing up for the three services we'll use in the workshop. We'll then move on to configuring Github Actions, Azure, and Octopus Deploy so that by the end of the workshop, you will have a complete CI/CD pipeline using Github Actions and Octopus Deploy, with all Infrastructure being deployed using Octopus Deploy Runbooks with Azure ARM Templates.

This workshop should always be led by a DevOps expert who can fill in any gaps during the workshop.

## Chapters

We will work through these in a specific order as the workshop has to be carried out for it all to work at the end. 

* [01_Summary](/Workshop/WorkshopGuide/01_Summary.md)
* [02_Prerequisites](/Workshop/WorkshopGuide/02_Prerequisites.md)
* [03_Github_Sign-up](/Workshop/WorkshopGuide/03_Github_Sign-up.md)
* [04_Octopus_Deploy_Cloud_Sign-up](/Workshop/WorkshopGuide/04_Octopus_Deploy_Cloud_Sign-up.md)
* [05_Azure_Sign_up](/Workshop/WorkshopGuide/05_Azure_Sign-up.md)
* [06_Azure_Infrastructure](/Workshop/WorkshopGuide/06_Azure_Infrastructure.md)
* [07_Azure_Service_Principal](/Workshop/WorkshopGuide/07_Azure_Service_Principal.md)
* [08_Github_Actions_Configuration](/Workshop/WorkshopGuide/08_Github_Actions_Configuration.md)
* [09_Octopus_Configuration](/Workshop/WorkshopGuide/09_Octopus_configuration.md)
* [10_Octopus_Runbooks](/Workshop/WorkshopGuide/10_Octopus_Runbooks.md)
* [11_Exection](/Workshop/WorkshopGuide/11_Execution.md)
* [12_Additional_Information](/Workshop/WorkshopGuide/12_Additional_Information.md)
* [13_WrapUp_Resources](/Workshop/WorkshopGuide/13_WrapUp_Resources.md)

## OctoPetShop

In this workshop, we will use OctoPetShop. You can see the entire repository on [Github](https://GitHub.com/octopussamples/octoPetShop). This version has been cut down for the requirements of this workshop. 

Octopus Pet Shop Example Web app written in .NET Core. This solution consists of:

 - Octopus Pet Shop Web front end
 - Product Service
 - Shopping Cart Service
 - Database project using Dbup

## Infrastructure as Code

This repository contains a mix of ARM and PowerShell for deploying resources to Microsoft Azure. You can see the ARM Templates and PowerShell scripts in the [Infrastructure Folder](Workshop/Infrastructure/), and you can see these in the [Create Infrastructure](Workshop/Infrastructure/Create_Infrastructure/) and [Destroy Infrastructure](Workshop/Infrastructure/Destroy_Infrastructure/) folders.

We will use [Octopus Runbooks](https://octopus.com/docs/runbooks) to provision all Infrastructure. No infrastructure will be deployed manually. 

You can see these in action by logging into [Octopus Deploy Webinar instance](https://webinar.octopus.app/app#/Spaces-142/projects/octopetshop/operations/runbooks) and looking at the [Create Infrastructure Runbook](https://webinar.octopus.app/app#/Spaces-142/projects/octopetshop/operations/runbooks/Runbooks-923) and the [Destroy Infrastructure Runbook](https://webinar.octopus.app/app#/Spaces-142/projects/octopetshop/operations/runbooks/Runbooks-924). 

Please pay particular attention to the [Octopus Variables](https://webinar.octopus.app/app#/Spaces-142/projects/octopetshop/variables) if you're following along by yourself, as these ARM templates are built to be used in Octopus using variables. 

## Accompanying Slides

You can see the accompanying slides [here](https://docs.google.com/presentation/d/1aza-OExmns_qYTIfPy_mfJJp1hsXnf6puLB9sxOv5pg/edit?usp=sharing) or [in the PDF in the Repository](DevOps_in_two_days_with_IaC,_Azure,_Github_Actions_and_Octopus_Deploy_Slides.pdf).

## Workshop Start

When ready, you can start with the [Workshop Summary](/Workshop/WorkshopGuide/01_Summary.md).

