# STC Rec - Hugo Static Site

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
