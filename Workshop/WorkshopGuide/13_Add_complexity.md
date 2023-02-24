# Add a more real world feel to your deployment

The deployment we have set up so far is a simple one, that wouldn't necessarily reflect a production or real world environment. 

The next steps are to make the deployment more realistic. 

## Add a Development Environment

- Head over to **Infrastructure**
- Select **Environments**
- Click **Add Environment**
- Add a new environment called **Development** and **Save**

## Configure the deployment lifecycle

Here we are going set up what Octopus Deploy call a lifecycle.  This is the process in which a deployment is promoted between your environments.  Typically a release would go to your development environment, and then your production environment. 

- Head over to **Library**
- Select **Lifecycles**
- Click on the **Default Lifecycle**
- Click on **Add Phase**
- Type in **Development** for the Phase Name
- Select **Add Environment**
- Select **Development** and ensure **Deploy automatically to this environment as soon as the release enters this phase** is checked and click **OK**
- Click on **Add Phase**
- Type in **Production** for the Phase Name
- Ensure **User will need to manually queue the deployment to this environment** is checked and click **OK**
- Click **Save**

💡💡 We have set it up so that a deployment goes to Development first and then Production. It is set that any new release that is issued will automatically trigger a deployment to Development, but we still need to manually deploy to Production. 💡💡

## Trigger an automatic release

We want to set it so that any new package that is pushed to Octopus Deploy's package repository triggers a release. 

This is typically what you would see within a real world deployment.  The software engineer makes a change to the code and builds that into a deployment package.  It is automatically pushed to the deployment tool and again automatically deployed to a development environment, for them to either test or the Testing team. 

- Head over to **Projects**
- Select the **Random Quotes** project
- Select **Triggers** under Deployments
- On the screen you will see a section say **Automatic Release Creation** with a **Setup** box below it, click on the **Setup** box
- When the configuration box pops up, select the **Deploy an Azure App Service** step and click **Save**

