# STC Rec - Hugo Static Site

As of August 6, 2025, this project is deployed as an Azure Static Web App at https://ashy-tree-0b6345b1e.2.azurestaticapps.net.  

I used the WRONG MS resource for deploying to the site listed above, but it worked.  For a Hugo site like this one perhaps https://learn.microsoft.com/en-us/azure/static-web-apps/publish-hugo is a better resrouce?  

## Azure Static Web App YAML Config

```yaml
name: Azure Static Web Apps CI/CD

on:
  push:
    branches:
      - main
  pull_request:
    types: [opened, synchronize, reopened, closed]
    branches:
      - main

jobs:
  build_and_deploy_job:
    if: github.event_name == 'push' || (github.event_name == 'pull_request' && github.event.action != 'closed')
    runs-on: ubuntu-latest
    name: Build and Deploy Job
    steps:
      - uses: actions/checkout@v3
        with:
          submodules: true
          lfs: false
      - name: Build And Deploy
        id: builddeploy
        uses: Azure/static-web-apps-deploy@v1
        with:
          azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN_ASHY_TREE_0B6345B1E }}
          repo_token: ${{ secrets.GITHUB_TOKEN }} # Used for Github integrations (i.e. PR comments)
          action: "upload"
          ###### Repository/Build Configurations - These values can be configured to match your app requirements. ######
          # For more information regarding Static Web App workflow configurations, please visit: https://aka.ms/swaworkflowconfig
          app_location: "/" # App source code path
          api_location: "" # Api source code path - optional
          output_location: "public" # Built app content directory - optional
          ###### End of Repository/Build Configurations ######

  close_pull_request_job:
    if: github.event_name == 'pull_request' && github.event.action == 'closed'
    runs-on: ubuntu-latest
    name: Close Pull Request Job
    steps:
      - name: Close Pull Request
        id: closepullrequest
        uses: Azure/static-web-apps-deploy@v1
        with:
          azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN_ASHY_TREE_0B6345B1E }}
          action: "close"
```




## Development

### Clone
Clone the project to your local workstation using:
```
git clone --recurse-submodules https://github.com/Tama-Toledo/stc-rec
```

The use of `--recurse-submodules` ensures that you get all active themes and any other _Git_ submodules that are part of the project.

#### Using _GitHub Desktop_
If you `clone` in some other manner without the `--recurse-submodules` flag, as is the case when using _GitHub Desktop_, be sure you also run the following:

```
cd ~/GitHub/stc-rec
git submodule init
git submodule update
```

If you don't do this your submodule(s), and therefore your _bootstrap\_bp\_hugo\_theme_, will be EMPTY!

### Create a New Branch
Use the following syntax to create a new local branch, and tracked upstream branch, on your workstation before you begin to make changes.
```
git checkout -b <new branch name>
```

## Developing Without Docksal
_Docksal_ is nice, but it's really overkill when it comes to developing with _Hugo_.  All you really need is an up-to-date version of _Hugo_ installed on your host.  Then, to develop a _Hugo_ project you need _Hugo_ running in a server mode ([Hugo Quickstart guide](https://gohugo.io/getting-started/quick-start/) for more details).

```
hugo server
```

`hugo server` starts a local _Hugo_ stack making the project available at [localhost:1313](http://localhost:1313).
The site updates as you edit, you don't even have to reload the page to see your changes.

**NOTE:** once started, the `hugo server` will run, blocking the console. Kill it with `Ctrl-C`, when you are done.

## Pushing to Production
This project is hosted on _GitHub Pages_, as such, all that you have to do to deploy your changes is to `git add`, `git commit -m`, and `git push` your changes to the `main` branch of the repo.

That essentially completes a push-to-production workflow.

The whole process can be run from the command-line like so:

```
cd ~/GitHub/stc-rec
git add .
git commit -m "Add commit message here"
git push
```
