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

GitHub Actions builds consist of **jobs** which in turn consist of **steps**.  By default, GitHub Actions jobs will run in parallel with each other while the steps within a job are executed sequentially.  It's possible to configure jobs to run sequentially using the `jobs.<job_id>.need` keyword. See the GitHub documentation on [Using jobs in a workflow](https://docs.github.com/actions/using-jobs/using-jobs-in-a-workflow) for more details.

Before defining the steps for your job, you must first tell GitHub Actions what type of runner to use. The [GitHub documentation](https://docs.github.com/actions/using-jobs/choosing-the-runner-for-a-job) explains the different types to choose from.

#### .NET Core build

The following example demonstrates a GitHub Actions build of our example application. This application is written in .NET Core. It consists of one part, a website. 

To build this application, you'll need the following steps:

- Checkout the source code
- Configure the runner with the appropriate versions of .NET core
- Build the solution
- Create folders to store published/compiled artifacts
- Publish each project to their respective artifact folders

Below is an example GitHub Actions workflow which includes these steps:

```yaml
name: .NET

env: 
  PACKAGE_ID: randomquotes-app

on:
  workflow_dispatch: {}

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3
    - name: Setup .NET ✨
      uses: actions/setup-dotnet@v2
      with:
        dotnet-version: |-
          3.1.x
          5.0.x
          6.0.x
    - name: Install Octopus Deploy CLI  🐙
      uses: OctopusDeploy/install-octopus-cli-action@v1.2.0
      with:
        version: latest
    - name: Restore dependencies
      run: dotnet restore
    - name: Build 🧱
      run: dotnet build --no-restore
    - name: Test 🧪
      run: dotnet test --no-build --verbosity normal
    - name: Publish application 🔖
      run: dotnet publish --configuration Release --no-restore --output "$GITHUB_WORKSPACE/artifacts/$PACKAGE_ID" $PROJECT_PATH
    - name: Create App Package 📦
      run: octo pack --id="$PACKAGE_ID" --format="Zip" --version="${{ github.run_number }}" --basePath="$GITHUB_WORKSPACE/artifacts/$PACKAGE_ID" --outFolder="$GITHUB_WORKSPACE/artifacts"
    - name: Push Random Quotes App Package to Octopus 🐙
      run: octo push --package="${{ github.workspace }}/artifacts/${{ env.PACKAGE_ID }}.${{ github.run_number }}.zip" --server="${{ secrets.OCTOPUS_SERVER_URL }}" --apiKey="${{ secrets.OCTOPUS_API_TOKEN }}" --space="${{ secrets.OCTOPUS_SPACE }}"
    - name: Generate Octopus Deploy build information 🐙
      uses: xo-energy/action-octopus-build-information@v1.4.9
      with:
        octopus_api_key: ${{ secrets.OCTOPUS_API_TOKEN }}
        octopus_project: Getting-Started
        octopus_space: ${{ secrets.OCTOPUS_SPACE }}
        octopus_server: ${{ secrets.OCTOPUS_SERVER_URL }}
        push_version: ${{ github.run_number }}
        push_package_ids: ${{ env.PACKAGE_ID }}
        push_overwrite_mode: OverwriteExisting
        output_path: octopus
```

### Create a workflow in your GitHub repository

To create a workflow within your GitHub repository follow these steps:

- Within your respository click on **Add File**
- Then click on **Create New File**
- Name the file **.github/workflows/dotnetbuild.yml**
- Within the file content copy the workflow example from above
- Click on commit new file

The workflow is now created, when you go into **Actions** within your respository you will be able to see it's run history and interact with it. 

**At this stage please trigger a run of the workflow.**

If you are comfortable with GitHub Actions and the steps detailed within this example you can jump to the [next step](09_Octopus_Deploy_Configuration.md), otherwise continue to read on as we'll walk through the workflow process and explain why each part was used.


## Explaining the workflow

The workflow has one job built within it, the short story is it builds the .NET application and packages it up and then ships it to Octopus Deploy for us to then deploy. 

If we break down the workflow into chunks. 

```yaml
name: .NET

env: 
  PACKAGE_ID: randomquotes-app

on:
  workflow_dispatch: {}
```

This first part sets up the workflow name and how it is triggered.  In this case we have set it so it gets manually triggered. 

The next part of the code defines the job, it's name and also the GitHub runner we want to use. 

```yaml
jobs:
  build:

    runs-on: ubuntu-latest

```

To package your artifacts for deployment, configure your build to use the `OctopusDeploy/install-octopus-cli-action` developed by Octopus Deploy by adding the following step (previous steps excluded for brevity):

```yaml
    - name: Install Octopus CLI
      uses: !include <image-version-install-octopus-cli-action>
      with:
        version: latest
```

The next part gets things ready on the runner for us to start to perform some actions.  It takes a copy of the code from our GitHub repository and checks it out into the working directory of the runner.  

It then installs dotnet and the Octopus Deploy CLI tools. 

```yaml
- uses: actions/checkout@v3
    - name: Setup .NET ✨
      uses: actions/setup-dotnet@v2
      with:
        dotnet-version: |-
          3.1.x
          5.0.x
          6.0.x
    - name: Install Octopus Deploy CLI  🐙
      uses: OctopusDeploy/install-octopus-cli-action@v1.2.0
      with:
        version: latest
```

The next part of the workflow starts to get the .NET application source code ready for deployment. 

```yaml
- name: Restore dependencies
      run: dotnet restore
    - name: Build 🧱
      run: dotnet build --no-restore
    - name: Test 🧪
      run: dotnet test --no-build --verbosity normal
    - name: Publish application 🔖
      run: dotnet publish --configuration Release --no-restore --output "$GITHUB_WORKSPACE/artifacts/$PACKAGE_ID" $PROJECT_PATH
```

To be able to deploy the application within Octopus Deploy it needs to be packaged as a zip file.  The next lines within the workflow zip the necessary files and then send them to the Octopus Deploy server.   You can see in the next few lines that the workflow is starting to call the secrets we created earlier. 

```yaml
- name: Create App Package 📦
      run: octo pack --id="$PACKAGE_ID" --format="Zip" --version="${{ github.run_number }}" --basePath="$GITHUB_WORKSPACE/artifacts/$PACKAGE_ID" --outFolder="$GITHUB_WORKSPACE/artifacts"
    - name: Push Random Quotes App Package to Octopus 🐙
      run: octo push --package="${{ github.workspace }}/artifacts/${{ env.PACKAGE_ID }}.${{ github.run_number }}.zip" --server="${{ secrets.OCTOPUS_SERVER_URL }}" --apiKey="${{ secrets.OCTOPUS_API_TOKEN }}" --space="${{ secrets.OCTOPUS_SPACE }}
```

## Next Section

Now that we have our workflow set up for the application build, we need to configure our deployment within Octopus Deploy. 

[Octopus Configuration](09_Octopus_Deploy_Configuration.md)