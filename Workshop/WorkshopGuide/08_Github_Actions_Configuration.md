#  Github Actions Configuration

[GitHub](https://github.com/) is a popular git-based source-control platform.

[GitHub Actions](https://github.com/features/actions) is GitHub's cloud-based continuous integration server.

The [GitHub-hosted runners](https://help.github.com/en/actions/getting-started-with-github-actions/core-concepts-for-github-actions#runner) require your Octopus Server to be accessible over the Internet.  Otherwise you must [self-host your runners](https://help.github.com/en/actions/hosting-your-own-runners).

## Octopus Deploy integrates with GitHub Actions

Octopus Deploy has several custom GitHub Actions available: 
- [Install Octopus CLI](https://github.com/marketplace/actions/install-octopus-cli)
- [Push packages](https://github.com/marketplace/actions/push-package-to-octopus-deploy)
- [Create a release](https://github.com/marketplace/actions/create-release-in-octopus-deploy)
- [Run a runbook](https://github.com/marketplace/actions/run-runbook-in-octopus-deploy)

All of the Actions are compatible with following runner types:

- Windows
- MacOS
- Linux
- Self-Hosted Runners

## Set up a GitHub Repository

The first step that we need to do is set up a GitHub repository that will hold our application source code and our build workflow.  We are going to copy or fork an existing respository. 

- Head over to [https://github.com/TechielassInc/RandomQuotes-Application](https://github.com/TechielassInc/RandomQuotes-Application/)
- Click on Fork in the top right hand corner
- Follow the prompts to create a new fork

Once it has been created, this your your own area to work within. 

The repository that you have forked has a copy of our Random Quotes application source code in it. 

## Configure GitHub Actions Secrets

GitHub Actions secrets are a great place to store sensitive information that can be used within your workflows. 

We are going to store three pieces of information in the secrets area. 

- Within the GitHub repository you have just created head over to **Settings**
- Select **Secrets and Variables**
- Then **Actions**
- Click on **New Repository Secret**
- Within the Name enter _OCTOPUSSERVERURL_
- Within the Secret enter the URL of your Octopus Deploy environment (don't add a trialing back slash)
- Click on Add Secret
- Click on **New Repository Secret**
- Within the Name enter _OCTOPUSSERVER_SPACE_
- Within the Secret enter Default (This is the default space name created within Octopus, we'll be utilising this for the purposes of this workspace, but best practice would be to create dedicated space per application or deployment)
- Click on Add Secret

The last secret is an API from Octopus Deploy that is required for GitHub and Octopus to talk to each other. 

- Logon to your Octopus Deploy environment
- Click on your name in the top right hand corner and select **Profile**
- Now click on **My API Keys**
- Create a new API Key
- Take a copy of the API key generated
- Head back to your GitHub Repository
- Click on Settings
- Select **Secrets and Variables**
- Then **Actions**
- Click on **New Repository Secret**
- Within the Name enter _OCTOPUSSERVERAPIKEY_
- Within the Secret enter the API key you just generated
- Click on Add Secret

**Best practice would be to create a service account, and assign it the correct permissions inside Octopus Deploy then create the API key as that Service Account and not follow the process of generating an API key to a users account. **




### Building with GitHub Actions

GitHub Actions builds consist of **jobs** which in turn consist of **steps**.  By default, GitHub Actions jobs will run in parallel with each other while the steps within a job are executed sequentially.  It's possible to configure jobs to run sequentially using the `jobs.<job_id>.need` keyword. See the GitHub documentation on [Using jobs in a workflow](https://docs.github.com/en/actions/using-jobs/using-jobs-in-a-workflow) for more details.

Before defining the steps for your job, you must first tell GitHub Actions what type of runner to use. The [GitHub documentation](https://docs.github.com/en/actions/using-jobs/choosing-the-runner-for-a-job) explains the different types to choose from.

```yaml
name: MyBuild

on:
  pull_request:
    branches: [ main ]
  schedule:
    - cron: "0 07 * * *"
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
```

#### Example .NET Core build

The following example demonstrates a GitHub Actions build of our example application, [OctoPetShop](https://github.com/OctopusSamples/OctoPetShop).  This application is written in .NET Core and consists of four components:

- OctopusSamples.OctoPetShop.Database - Database updates using DBUp
- OctopusSamples.OctoPetShop.Web - Web front end
- OctopusSamples.OctoPetShop.ProductService - Product service API
- OctopusSamples.OctoPetShop.ShoppingCartService - Shopping cart service API

To build this application, you'll need the following steps:

- Checkout the source code
- Configure the runner with the appropriate version of .NET core
- Restore any NuGet packages required by the solution
- Build the solution
- Create folders to store published/compiled artifacts
- Publish each project to their respective artifact folders

Below is an example GitHub Actions workflow which includes these steps:

```yaml
name: MyBuild

on:
  pull_request:
    branches: [ main ]
  schedule:
    - cron: "0 07 * * *"
  workflow_dispatch:

jobs:
  build:

    runs-on: ubuntu-latest    
    
    steps:
    - uses: actions/checkout@v2
    - name: Set Version
      run: echo "PACKAGE_VERSION=$(date +'%Y.%m.%d').$GITHUB_RUN_NUMBER" >> $GITHUB_ENV
    - name: Setup .NET Core
      uses: actions/setup-dotnet@v1
      with:
        dotnet-version: 2.2.207
    - name: Install dependencies
      run: dotnet restore
    - name: Build
      run: dotnet build --configuration Release --no-restore
    - name: Create artifacts folder
      run: |
        mkdir "$GITHUB_WORKSPACE/artifacts"
        mkdir "$GITHUB_WORKSPACE/artifacts/OctopusSamples.OctoPetShop.Database"
        mkdir "$GITHUB_WORKSPACE/artifacts/OctopusSamples.OctoPetShop.Web"
        mkdir "$GITHUB_WORKSPACE/artifacts/OctopusSamples.OctoPetShop.ProductService"
        mkdir "$GITHUB_WORKSPACE/artifacts/OctopusSamples.OctoPetShop.ShoppingCartService"
    - name: Publish OctoPetShopDatabase
      run: dotnet publish OctopusSamples.OctoPetShop.Database/OctopusSamples.OctoPetShop.Database.csproj --configuration Release --no-restore --output "$GITHUB_WORKSPACE/artifacts/OctopusSamples.OctoPetShop.Database"
    - name: Publish OctoPetShopWeb
      run: dotnet publish OctopusSamples.OctoPetShop.Web/OctopusSamples.OctoPetShop.Web.csproj --configuration Release --no-restore --output "$GITHUB_WORKSPACE/artifacts/OctopusSamples.OctoPetShop.Web"
    - name: Publish OctoPetShopProductService
      run: dotnet publish OctopusSamples.OctoPetShop.ProductService/OctopusSamples.OctoPetShop.ProductService.csproj --configuration Release --no-restore --output "$GITHUB_WORKSPACE/artifacts/OctopusSamples.OctoPetShop.ProductService"
    - name: Publish OctoPetShopShoppingCartService
      run: dotnet publish OctopusSamples.OctoPetShop.ShoppingCartService/OctopusSamples.OctoPetShop.ShoppingCartService.csproj --configuration Release --no-restore --output "$GITHUB_WORKSPACE/artifacts/OctopusSamples.OctoPetshop.ShoppingCartService"
```

### Packaging artifacts

To package your artifacts for deployment, configure your build to use the `OctopusDeploy/install-octopus-cli-action` developed by Octopus Deploy by adding the following step (previous steps excluded for brevity):

```yaml
    - name: Install Octopus CLI
      uses: !include <image-version-install-octopus-cli-action>
      with:
        version: latest
```

Adding this Action allows your build to use the commands from the Octopus [command line interface (CLI)](/docs/octopus-rest-api/octopus-cli/index.md).  Using the [pack](/docs/octopus-rest-api/octopus-cli/pack.md) command, you can package your artifacts for deployment.  The following example packages the OctoPetShop components built above:

```yaml
    - name: Install Octopus CLI
      uses: !include <image-version-install-octopus-cli-action>
      with:
        version: latest
    - name: Package OctoPetShopDatabase
      run: |
        octo pack --id="OctoPetShop.Database" --format="Zip" --version="$PACKAGE_VERSION" --basePath="$GITHUB_WORKSPACE/artifacts/OctopusSamples.OctoPetShop.Database" --outFolder="$GITHUB_WORKSPACE/artifacts"
    - name: Package OctoPetShopWeb
      run: |
        octo pack --id="OctoPetShop.Web" --format="Zip" --version="$PACKAGE_VERSION" --basePath="$GITHUB_WORKSPACE/artifacts/OctopusSamples.OctoPetShop.Web" --outFolder="$GITHUB_WORKSPACE/artifacts"
    - name: Package OctoPetShopProductService
      run: |
        octo pack --id="OctoPetShop.ProductService" --format="Zip" --version="$PACKAGE_VERSION" --basePath="$GITHUB_WORKSPACE/artifacts/OctopusSamples.OctoPetShop.ProductService" --outFolder="$GITHUB_WORKSPACE/artifacts"
    - name: Package OctoPetShopShoppingCartService
      run: |
        octo pack --id="OctoPetShop.ShoppingCartService" --format="Zip" --version="$PACKAGE_VERSION" --basePath="$GITHUB_WORKSPACE/artifacts/OctopusSamples.OctoPetshop.ShoppingCartService" --outFolder="$GITHUB_WORKSPACE/artifacts"
```

### Pushing artifacts to Octopus Server

Once the artifacts are packaged, use the **OctopusDeploy/push-package-action** Action to push the packages to the Octopus Server built-in repository.  The following example pushes the packages created from the previous `pack` operation:

```yaml
    - name: Push OctoPetShop packages
      uses: OctopusDeploy/push-package-action@v1.1.1
      with:
        api_key: ${{ secrets.OCTOPUSSERVERAPIKEY }}
        server: ${{ secrets.OCTOPUSSERVERURL }}
        packages: "artifacts/OctoPetShop.Database.${{ env.PACKAGE_VERSION }}.zip,artifacts/OctoPetShop.Web.${{ env.PACKAGE_VERSION }}.zip,artifacts/OctoPetShop.ProductService.${{ env.PACKAGE_VERSION }}.zip,artifacts/OctoPetShop.ShoppingCartService.${{ env.PACKAGE_VERSION }}.zip"
        space: ${{ secrets.OCTOPUSSERVER_SPACE }}
```

### Creating a release

To create a release, use the **OctopusDeploy/create-release-action**.  This action also contains the ability to deploy the newly created release.  Use either the `progress` or `wait_for_deployment` options to have the build wait for the deployment to complete and report success or failure. Using  `progress` will display messages from Octopus itself whereas `wait_for_deployment` will simply wait for Octopus to report success or failure.:

```yaml
    - name: Create and deploy release
      uses: OctopusDeploy/create-release-action@v1.1.1
      with:
        api_key: ${{ secrets.OCTOPUSSERVERAPIKEY }}
        server: ${{ secrets.OCTOPUSSERVERURL }}
        space: ${{ secrets.OCTOPUSSERVER_SPACE }}
        project: "Octo Pet Shop"
        deploy_to: "Development"
        progress: true
```

The variable **PACKAGE_VERSION** must be referenced like **${{ env.PACKAGE_VERSION }}** for both **push-package-action** and **create-release-action**

### Complete build example
The previous sections displayed only the portions relavent to the topic being discussed.  The entire build YAML for the Octo Pet Shop is located below:

<details>
  <summary>Click here to view the entire example build YAML</summary>

```yaml
name: MyBuild

on:
  pull_request:
    branches: [ main ]
  schedule:
    - cron: "0 07 * * *"
  workflow_dispatch:
    logLevel:
      description: 'Log level'
      required: true
      default: 'warning'

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
    - name: Set Version
      run: echo "PACKAGE_VERSION=$(date +'%Y.%m.%d').$GITHUB_RUN_NUMBER" >> $GITHUB_ENV
    - name: Setup .NET Core
      uses: actions/setup-dotnet@v1
      with:
        dotnet-version: 2.2.207
    - name: Install dependencies
      run: dotnet restore
    - name: Build
      run: dotnet build --configuration Release --no-restore
    - name: Test
      run: dotnet test --no-restore --verbosity normal
    - name: Create artifacts folder
      run: |
        mkdir "$GITHUB_WORKSPACE/artifacts"
        mkdir "$GITHUB_WORKSPACE/artifacts/OctopusSamples.OctoPetShop.Database"
        mkdir "$GITHUB_WORKSPACE/artifacts/OctopusSamples.OctoPetShop.Web"
        mkdir "$GITHUB_WORKSPACE/artifacts/OctopusSamples.OctoPetShop.ProductService"
        mkdir "$GITHUB_WORKSPACE/artifacts/OctopusSamples.OctoPetShop.ShoppingCartService"
    - name: Publish OctoPetShopDatabase
      run: dotnet publish OctopusSamples.OctoPetShop.Database/OctopusSamples.OctoPetShop.Database.csproj --configuration Release --no-restore --output "$GITHUB_WORKSPACE/artifacts/OctopusSamples.OctoPetShop.Database"
    - name: Publish OctoPetShopWeb
      run: dotnet publish OctopusSamples.OctoPetShop.Web/OctopusSamples.OctoPetShop.Web.csproj --configuration Release --no-restore --output "$GITHUB_WORKSPACE/artifacts/OctopusSamples.OctoPetShop.Web"
    - name: Publish OctoPetShopProductService
      run: dotnet publish OctopusSamples.OctoPetShop.ProductService/OctopusSamples.OctoPetShop.ProductService.csproj --configuration Release --no-restore --output "$GITHUB_WORKSPACE/artifacts/OctopusSamples.OctoPetShop.ProductService"
    - name: Publish OctoPetShopShoppingCartService
      run: dotnet publish OctopusSamples.OctoPetShop.ShoppingCartService/OctopusSamples.OctoPetShop.ShoppingCartService.csproj --configuration Release --no-restore --output "$GITHUB_WORKSPACE/artifacts/OctopusSamples.OctoPetshop.ShoppingCartService"
    - name: Install Octopus CLI
      uses: OctopusDeploy/install-octopus-cli-action@v1.1.6
      with:
        version: latest
    - name: Package OctoPetShopDatabase
      run: |
        octo pack --id="OctoPetShop.Database" --format="Zip" --version="$PACKAGE_VERSION" --basePath="$GITHUB_WORKSPACE/artifacts/OctopusSamples.OctoPetShop.Database" --outFolder="$GITHUB_WORKSPACE/artifacts"
    - name: Package OctoPetShopWeb
      run: |
        octo pack --id="OctoPetShop.Web" --format="Zip" --version="$PACKAGE_VERSION" --basePath="$GITHUB_WORKSPACE/artifacts/OctopusSamples.OctoPetShop.Web" --outFolder="$GITHUB_WORKSPACE/artifacts"
    - name: Package OctoPetShopProductService
      run: |
        octo pack --id="OctoPetShop.ProductService" --format="Zip" --version="$PACKAGE_VERSION" --basePath="$GITHUB_WORKSPACE/artifacts/OctopusSamples.OctoPetShop.ProductService" --outFolder="$GITHUB_WORKSPACE/artifacts"
    - name: Package OctoPetShopShoppingCartService
      run: |
        octo pack --id="OctoPetShop.ShoppingCartService" --format="Zip" --version="$PACKAGE_VERSION" --basePath="$GITHUB_WORKSPACE/artifacts/OctopusSamples.OctoPetshop.ShoppingCartService" --outFolder="$GITHUB_WORKSPACE/artifacts"
    - name: Push OctoPetShop packages
      uses: OctopusDeploy/push-package-action@v1.1.1
      with:
        api_key: ${{ secrets.OCTOPUSSERVERAPIKEY }}
        server: ${{ secrets.OCTOPUSSERVERURL }}
        packages: "artifacts/OctoPetShop.Database.${{ env.PACKAGE_VERSION }}.zip,artifacts/OctoPetShop.Web.${{ env.PACKAGE_VERSION }}.zip,artifacts/OctoPetShop.ProductService.${{ env.PACKAGE_VERSION }}.zip,artifacts/OctoPetShop.ShoppingCartService.${{ env.PACKAGE_VERSION }}.zip"
        space: ${{ secrets.OCTOPUSSERVER_SPACE }}
    - name: Create and deploy release
      uses: OctopusDeploy/create-release-action@v1.1.1
      with:
        api_key: ${{ secrets.OCTOPUSSERVERAPIKEY }}
        server: ${{ secrets.OCTOPUSSERVERURL }}
        space: ${{ secrets.OCTOPUSSERVER_SPACE }}
        project: "Octo Pet Shop"
        deploy_to: "Development"
        progress: true
```
</details>


### Run a runbook
In addition to common build steps, we also have an action that can Run a Runbook.

```yaml
  - name: Run a runbook in Octopus Deploy
    uses: OctopusDeploy/run-runbook-action@1.0.1
    with:
      api_key: ${{ secrets.OCTOPUSSERVERAPIKEY }}
      environments: 'Development'
      project: 'Octo Pet Shop'
      runbook: 'Restart IIS App pool'
      server: ${{ secrets.OCTOPUSSERVERURL }}
      space: ${{ secrets.OCTOPUSSERVER_SPACE }}
      show_progress: 'true'
```

**Example GitHub Actions Repo:**

- [.NET Core](https://github.com/OctopusSamples/OctoPetShop/blob/master/.github/workflows/dotnet-core.yml)
- [Java using Maven](https://github.com/OctopusSamples/RandomQuotes-Java/blob/master/.github/workflows/maven.yml)
- You can see our example [.NET Core here](https://github.com/OctopusDeployCommunity//blob/main/.github/workflows/dotnet-core-build.yml)


## Github Actions Workflow Demo

Octopus have created free tool to build your [Github Actions Workflow generator](https://githubactionsworkflowgenerator.octopus.com/#/) without the need for writing any YAML. 

Test it out with your example and see it compares with the one that's already been generated for you. 

## Next Section

[Octopus Configuration](09_Octopus_Deploy_Configuration.md)