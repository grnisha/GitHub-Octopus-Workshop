#  Execution Instructions

It's now time to deploy our application to the infrastructure we've deployed.  Let's do some checks before we do that though. 

## Checks

- Head over to **Infrastructure**
- Ensure that you have a **Healthy** deployment target available to you. _If not you may not have successfully deployed your **Create Infrastructure** Runbook_
- Next head over to **Library** 
- Ensure within the **Packages** are you have a _randomquotes-app_ package there for deployment. _If not you may your GitHub Actions workflow might have failed to deploy successfully_

## Deployment

- Head over to **Projects**
- Select the **Randoms Quotes** project you have set up
- Click on **Create release**
- Octopus will automatically give your release a number, in this case it should be 0.0.1.  In the summary box you will see that it has picked up your source code package.  And there is also a section for release notes, you can add any relevant information for looking back on here. 
- Click **Save**
- You will be taken to another summary page which will give you more information about the release and how it will deployed.   At this stage if you had multiple environments you would see them here and depending on how your team is set up you might only have rights to deploy to a certain environment.  We only have one environment set up at the moment.  Click on **Deploy to Production**
- Then click on **Deploy**
- The deployment process will now start to deploy the source code to the web app.  If the deployment is successful you should see green ticks next to each step.  The **Task Log** for the deployment can be used to troubleshoot or look into the process in more depth. 