#  Octopus Configuration

## Adding Environments

Since environments are the phases you move your code through, they form the backbone of your deployment pipeline. Before you configure anything else, you should configure your environments.

The most common setup is four environments. These are:

1. **Development** - is for developers to experiment on. It's generally in flux and can often be expected to be unavailable.
1. **Test/QA** - Quality assurance teams test functionality in the test environment.
1. **Staging/Pre-Production** - Staging is used as a final sanity check before deploying to Production.
1. **Production** is where your end users usually use your software outside testing.

Some companies only have three environments. Others have many more. Likewise, not everyone names their environments the same way. One person's Test is another person's QA. It's essential that you can call your environments in the way that best supports your organization's needs.

### Adding your environment

In our example, we will configure a single environment of **Production**. 

- Logon to your Octopus instance
- Browse to Infrastructure -> Environments
- Select **Add environment**
- A small window should pop up. Input **Production** for the name. 
- Please ensure **Dynamic Infrastructure** is set yes. 

## Projects

Projects let you create and manage your deployment processes, releases, and runbooks from the Octopus REST API and Octopus Web Portal.

For each project, you can define a deployment process, runbooks to manage your Infrastructure, variables, the environments where the software will be deployed, and releases of your software.

You can manage your projects by navigating to the Projects tab in the Octopus Web Portal:

## Add a project

Before you can define your deployment processes or runbooks, you must create a project:

1. Select **Projects** from the main navigation and click **ADD PROJECT**.
1. Name it **RandomQuotes-YOURINITIALS**. _Replace YOURINITIALS with your own initials, such as SL_

## Project settings

You can change the project's settings by accessing the main page's settings menu. The settings you can change are:

- Name.
- Enable or disable the project to allow or prevent releases and deployments from being created.
- [Logo](#project-logo)
- Description
- [Project Group](#project-group)
- [Release Versioning](/docs/releases/release-versioning.md)
- [Release Notes Template](/docs/releases/release-notes.md#Release-Notes-Templates)


## Project logo {#project-logo}

Customize your project logo to make it easily identifiable amongst other projects.

1. From the project's main page, select **Settings**.
2. Click the **Logo** section of the settings page.
3. Select from our built-in icon library paired with your choice of color or upload a custom image.
4. Click **Save**.

For custom images, in addition to supporting .jpg and .png files, we also support .gif files. This means you can have an animated icon to add a little flair to your Octopus Deploy instance!

## Variable Setup

### Global Variable Set Setup

[Library Variable Sets](https://octopus.com/docs/projects/variables/library-variable-sets) is a way for you to define variables across multiple projects. In our example, we're going to define a **Global Variable Set** to be used for all Projects inside of Octopus.

- Browse to Library-> Variable Sets
- Create a Variable Set named **Global**
- Create a Variable called **Global.API.Key** and use the API key you generated earlier. 
- Create a Variable called **Global.Base.URL** and use the URL of your Octopus instance, with a backslash at the end. If you created one name **techielassinc.octopus.app/** then this is what you'd input. 
- Create a Variable called **Global.Environment.Prefix** and input **p** and scope it to the Production environment.
- Create a Variable called **Global.Environment.Suffix** and input **prod** and scope it to the Production environment.
- Create a Variable called **Global.Server.Thumbprint** and input your Octopus Server Thumbprint. You can get this from Octopus->Configuration->Thumbprint

_Do remember to hit Save once you have inputted the variables before leaving the screen_

### Azure Variable Set setup

In this section, we will now define the Azure Variable Set, which can be used by all of your Projects, as we're only defining a single Project that could easily be used in the Project variables, but let's set ourselves up for success and scalability!

We're deliberately going to leave one Variable out for the time being, and we'll come back to that later after we have set up Azure.

- Browse to Library-> Variable Sets
- Create a Variable Set named **Azure**
- Create a Variable called **Azure.Account.Name**, click on _Open Editor_, select Variable type and select _Azure Account_, select your Azure subscription and click on Done
- Create a Variable called **Azure.Location.Abbr** and input **uksouth**
- Create a Variable called **Azure.Location.Name** input **UK South**
- Create a Variable called **Azure.ResourceGroup.Name** and input **#{Octopus.Space.Name | ToLower | Replace " "}-#{Octopus.Project.Name | ToLower | Replace " "}-#{Octopus.Environment.Name | ToLower}-rg**.
- Create a Variable called **Azure.webSiteName** and input **#{Octopus.Space.Name | ToLower | Replace " "}-#{Octopus.Project.Name | ToLower | Replace " "}-#{Octopus.Environment.Name | ToLower}-frontend**
- Create a Variable called **Azure.appname** and input **#{Octopus.Space.Name | ToLower | Replace " "}-#{Octopus.Project.Name | ToLower | Replace " "}-#{Octopus.Environment.Name | ToLower}-asp**
- Create a Variable called **Azure.skucode** and input **S1**
- Create a Variable called **Azure.osType** and input **windows**

### Project Variables

In this section, we will now define the [Project Variables](https://octopus.com/docs/projects/variables). We are mixing Project and Library Variable sets as this is more real world. Still, these variables could be either in the Library Variable Set or as Project Variables.

- Browse to your project -> Variables -> Variables
- Create a Variable called **AppSettings:AppVersion** input **#{Octopus.Release.Number}**
- Create a Variable called **AppSettings:EnvironmentName** and input **#{Octopus.Environment.Name}**

### Add Library Variable Sets to your project

- Browse your project
- Under **Variables** please select **Library Set**
- Select the button called **Include Library Variable Sets**
- Select both your **Global** and **Azure** Library Variable Sets
- You can now use the Variables in the Variable Set as part of your projects. Without this, you would only have access to the Project Variables

Your Octopus Deployment process is now completed.

