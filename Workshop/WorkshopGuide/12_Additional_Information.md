# NDCDevOpsWorkshop Additional Information

## Config as Code

The [Configuration as Code (config-as-code)](https://octopus.com/docs/projects/version-control) feature adds support for configuring Octopus projects to store project resources in a Git repository. Only the deployment process and some deployment settings can be version-controlled.

The Octopus UI needed to remain fully functional for version-controlled projects, and it has. You can continue to use the UI precisely as you always have. Still, with an additional super-power: Git branches are now exposed in the UI, allowing editing of the deployment process on any branch via the UI. If you type the name of a branch that doesn't exist in your repository, you'll see an option to create that branch. This option is available when committing changes to your deployment process too.

You can see a webinar about Config as Code on [YouTube](https://www.youtube.com/watch?v=Z4DgiJ630FU). 

If there's enough time, we will do class-led instructions using Config as Code, but why not give it a try yourself?

### Git Credentials for Config as Code

- Browse to **Library**
- Select **Git Credentials**
- Select **Add Git Credentials**
- Name it **Git Service Account**
- Input your Github Username
- [Create a personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)
- Take note of the token and paste it into the Git Credentials and test. 

### Project Configuration

- Go to **Settings -> Version Control**
- Input the git Repository URL
- Select **main**
- Select your Service Account
- Keep the rest as default
- Select **test**, and it should work
- Config as Code is now completed. 

### Installing the Octopus Deploy VSCode extension

- Install VSCode if you don't have it. 
- Browse to https://marketplace.visualstudio.com/items?itemName=octopusdeploy.vscode-octopusdeploy
- Install the extension locally or try it using Github CodeSpaces by pressing . in your browser when in Github.

## Channels

You can watch a webinar about channels and lifecycles on [YouTube](https://www.youtube.com/watch?v=y_cS_DL4CcY).

As you deploy your projects, you can assign releases of projects to specific channels. This is useful when you want releases of a project to be treated differently depending on the criteria you've set. Without channels, you could duplicate projects to implement multiple release strategies. This would, of course, leave you trying to manage various duplicated projects. Channels let you use one project with multiple release strategies.

Channels can be helpful in the following scenarios:

* Feature branches (or experimental branches) are deployed to test environments, not Production.
* Early access versions of the software are released to members of your early access program.
* Hotfixes are deployed straight to Production and then through the rest of your infrastructure after the fix has been released.

When you are implementing a deployment process that uses channels, you can scope the following to specific channels:

* Lifecycles
* Steps
* Variables
* Tenants

You can also define versioning rules per channel to ensure that only versions that meet specific criteria are deployed to particular channels.

Read more about [channels](https://octopus.com/docs/deployment-process/channels).

## Lifecycles

You can watch a webinar about channels and lifecycles on [YouTube](https://www.youtube.com/watch?v=y_cS_DL4CcY)

Lifecycles give you control over the way releases of your software are promoted between your environments. Lifecycles enable several advanced deployment workflow features:

* Control the order of promotion: for example, to prevent a release from being deployed to Production if it hasn't been deployed to staging.
* Automate deployment to specific environments: for example, automatically deploy to test as soon as a release is created.
* Retention policies: specify the number of releases to keep depending on how far they have progressed through the lifecycle.

Phases define lifecycles. A lifecycle can have one or many stages.

* Phases occur in order. One phase must have a complete, successful deployment before the release is deployed to the next phase.
* Phases have one or more environments.
* Environments in a phase can be defined as automatic or manual deployment environments.
* Phases can have a set number of environments that must be released before the next phase is available for deployment.

You can specify multiple lifecycles to control which projects are deployed to which environments.

Lifecycles are managed from the library page by navigating to Library ➜ Lifecycles:

Lifecycles are a crucial channel component that gives you even greater control over how your software is deployed. Channels let you use multiple lifecycles for a project and then automatically deploy to specific channels, using the defined lifecycle based on the version of the software being deployed.

You can read more [lifecycles](https://octopus.com/docs/deployment-process/lifecycles)

## Multi-Tenancy

You can watch a webinar about multi-tenanted deployments with Octopus Deploy on [YouTube](https://www.youtube.com/watch?v=qsHSosC3GmA).

This section describes how to use Octopus to manage deployments of your applications to multiple end customers.

Consider the following scenario:

NameBadge makes HR software for large corporate customers. They provide the software as a SaaS offering to their customers and host the website and associated services. Due to how the application is structured, for each customer, they deploy:

* A different SQL database.
* A copy of an ASP.NET website.
* A copy of a Windows Service.

The critical issue in this scenario is that the same components must be deployed multiple times, once for each end customer.

1. Deploy multiple instances of your project into the same [environment](/docs/infrastructure/environments/index.md);

* Tenant-per-customer
* Tenant-per-tester
* Tenant-per-feature/tenant-per-branch
* Tenant-per-geographical-region
* Tenant-per-datacenter

2. Easily manage unique configuration settings using variables defined on the tenant.
3. Promote releases to your tenants using safe customer-aware lifecycles, potentially through multiple environments:

* Tenant-specific UAT and Production environments.

4. Tailor the deployment process of your projects per-tenant as necessary.
5. Implement dedicated or shared hosting models for your tenants.
6. Employ tenant-aware security for managing tenants and deploying projects, including 3rd-party self-service sign-in.
7. Implement early access or pre-release test programs incorporating 1st-party or 3rd-party testers.
8. Easily scale to large numbers of tenants using tags to manage tenants as groups instead of individuals.
9. Easily implement simple multi-tenant deployment scenarios and scale to support complex scenarios as your needs require.

Read more about [multi-tenancy](https://octopus.com/docs/deployment-patterns/multi-tenant-deployments).

## Spaces

You can watch a webinar about Spaces on [YouTube](https://youtu.be/EJgM0r58VDc?t=278)

With Spaces, you can partition your Octopus Deploy Server so that each team can only access the projects, environments, and infrastructure they work with from the spaces they are members of. Users can be members of multiple teams and have access to various spaces, but the entities and infrastructure they work with will only be available in the space it is assigned to.

Read more about [Spaces](https://octopus.com/docs/administration/spaces)

### Workers

You can watch a webinar about Workers on [YouTube](https://youtu.be/EJgM0r58VDc?t=1697)

Workers are machines that can execute tasks that don't need to be run on the Octopus Server or individual deployment targets.

You can manage your Workers by navigating to infrastructure ➜ Worker Pools in the Octopus Web Portal. Workers are helpful for the following scenarios:

* Publishing to Azure websites.
* Deploying AWS CloudFormation templates.
* Deploying to AWS Elastic Beanstalk.
* Uploading files to Amazon S3.
* Backing up databases.
* Performing database schema migrations
* Configuring load balancers.

Read more about [Workers](https://octopus.com/docs/infrastructure/workers).

## Common Deployment Patterns

### Blue/Green

Blue-green deployments are a pattern that reduces downtime during production deployments by having two production environments ("blue" and "green").

> One of the challenges with automating deployment is the cut-over, taking software from the final testing stage to live Production. It would help if you usually did this quickly to minimize downtime. The **blue-green deployment** approach ensures you have two production environments as identical as possible. At any time, one of them, say blue, for example, is live. As you prepare a new release of your software, you do your final testing stage in the green environment. Once the software works in the green environment, you switch the router so that all incoming requests go to the green environment - the blue one is now idle.
>
> * [Martin Fowler](http://martinfowler.com/bliki/BlueGreenDeployment.html)

As well as reducing downtime, Blue/Green can be a powerful way to use extra hardware compared to having a dedicated staging environment:

* Staging: When blue is active, green becomes the staging environment for the next deployment.
* Rollback: We deploy to blue and make it active. Then a problem is discovered. Since green still runs the old code, we can roll back easily.
* Disaster recovery: After deploying to blue and we're satisfied that it is stable, we can deploy the new release to green too. This gives us a standby environment ready in case of disaster.

Read more about [blue/green deployments](https://octopus.com/docs/deployment-patterns/blue-green-deployments).

### Red/Black

When deploying new versions of a centralized application like a web service, there is a strategy you can use to direct production traffic to the latest version only after it has been successfully deployed and optionally tested. This strategy goes by the name blue/green or red/black, with each color representing a copy of the target environment. Traffic is routed to one color or the other (or potentially both in a canary deployment or during A/B testing, but that's a story for another time). Having two environments running side by side and hosting different versions of an application means traffic can be switched over and back again if an issue is found, with little to no downtime.

So why is this strategy referred to as green/blue and red/black? Do these colors imply technical differences?

StackOverflow says

Our first stop is StackOverflow, where we find the question [What's the difference between Red/Black deployment and Blue/Green Deployment?](https://stackoverflow.com/questions/45259589/whats-the-difference-between-red-black-deployment-and-blue-green-deployment).

The highest voted answer indicates that there is indeed a difference between these two terms:

> in blue-green deployment, both versions may be getting requests at the same time temporarily, while in red-black, only one of the versions is getting traffic at any point in time

The answer then goes on to say that:

> But red-black deployment is a newer term being used by Netflix, Istio, and other frameworks/platforms that support container orchestration

I've frequently seen the term red/black being attributed to tools created by Netflix and container platforms, so let's go to their documentation to see how they define these strategies.

Read more about [Red/Black(<https://octopus.com/blog/blue-green-red-black).>

### Canary Deployments

Canary deployments are a pattern for rolling out releases to a subset of users or servers. The idea is first to deploy the change to a small subset of servers, test it, and then roll it out to the rest of the servers. The canary deployment serves as an early warning indicator with less impact on downtime; if the canary deployment fails, the rest of the servers aren't impacted.

> Canaries were once regularly used in [coal mining](http://en.wikipedia.org/wiki/Coal_mining "Coal mining") as an early warning system. [Toxic](http://en.wikipedia.org/wiki/Toxic "Toxic") [gases](http://en.wikipedia.org/wiki/Gas "Gas") such as [carbon monoxide](http://en.wikipedia.org/wiki/Carbon_monoxide "Carbon monoxide"), [methane](http://en.wikipedia.org/wiki/Methane "Methane") or [carbon dioxide](http://en.wikipedia.org/wiki/Carbon_dioxide "Carbon dioxide") in the mine would kill the bird before affecting the miners. Signs of distress from the bird indicated to the miners that conditions were unsafe. The use of miners' canaries in [British](http://en.wikipedia.org/wiki/Great_Britain "Great Britain") mines was phased out in 1987.
>
> * [Wikipedia](http://en.wikipedia.org/wiki/Domestic_Canary#Miner.27s_canary)

The necessary steps of a canary deployment are:

1. Deploy to one or more canary servers.
2. Test or wait until satisfied.
3. Deploy to the remaining servers.

The test phase of the canary deployment can work in many ways. You could run some automated tests, perform manual testing, or even leave the server live and wait to see if end-users encounter problems. All three of these approaches might be used. Depending on how you plan to test, you might decide to remove the canary server from the production load balancer and return it only when rolling out the change to the rest of the servers.

**Similar to staging**
Canary deployments are similar to using a staging environment. The difference is that staging environments are usually dedicated to the task; a staging web server doesn't become a production server. By contrast, in a canary deployment, the canary server remains part of the production fleet when the deployment is complete. Canary deployments may be worth considering if you do not have the resources for a dedicated staging environment.

Read more about [Canary Deployments](https://octopus.com/docs/deployment-patterns/canary-deployments).

## Octopus 

* [Auditing](https://octopus.com/docs/administration/managing-users-and-teams/auditing).
* [External Authentication Providers](https://octopus.com/docs/administration/authentication).
* [Users/Teams/Permissions](https://octopus.com/docs/administration/managing-users-and-teams).
* [Upgrading Octopus](https://octopus.com/docs/administration/upgrading).
* [Retention Policies](https://octopus.com/docs/administration/retention-policies).
* [Cloud vs On-Premise](https://octopus.com/docs/octopus-cloud).

## Next Section

[WrapUp Resources](13_WrapUp_Resources.md)