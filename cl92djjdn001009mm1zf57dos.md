# Exploring Napptive GitHub Actions

**Hey everyone, I am Hasnain Makada currently working as a Developer Advocate at [Napptive](https://napptive.com) where I explore the platform deeply and educate the community about DevOps and Flutter. Today I am going to show the custom GitHub actions by napptive with which you can speed up the integration of CI/CD pipelines to execute tests on the platform**

So without waiting for any further ado, Let's get started

## Generating personal access token

To start with the actions, you first need to generate your personal access token from the napptive playground. To generate the unique access token, make sure that you have the **[CLI](https://docs.napptive.com/getting_started/starting_with_the_cli.html)** installed on your machine.

Open your terminal and run this command to generate a token.
```
playground user pat create ci_pat
```
After running this command your token will be generated successfully and visible to you inside your terminal. Make sure to save it so that you don't lose it.

Now save the access token inside your [github secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets#creating-encrypted-secrets-for-a-repository) and name it `PLAYGROUND_PAT` and you're good to go.

## What are Napptive GitHub Actions?

Napptive has provided a set of GitHub actions with which we can automate various tasks such as listing all the catalogues from the playground, deploying catalogues, pushing applications to the playground etc...

If you don't know about what are GitHub Actions, make sure to check out [this blog](https://hasnainm.hashnode.dev/github-actions)

Currently, Napptive provides 2 actions to automate the stuff. With these actions, you can basically perform the normal tasks mentioned above

* **playground-github-action**
* **catalog-deploy-action**

So let's see how to integrate all the above three into our repository

### Playground GitHub Action

The `playground-github-action` allows you to execute any playground command you need, To explore all the commands used check out [this link](https://docs.napptive.com/playground/cli/environments.html#environments).

To get started with the actions create a `.github/workflows` directory inside your main repository to define all your workflows over there.

Now create a `playground-github-action.yml` file inside  `workflows` directory and paste this code inside the file.
```
name: List deployed applications
on: [push]
jobs:
  deploy:
    name: Playground List applications
    runs-on: ubuntu-latest
    steps:
      # Get a copy of the repo.
      - uses: actions/checkout@v2
      # Execute `playground apps `.
      - uses: napptive-actions/playground-github-action@v4.1.0
        env:
          PLAYGROUND_PAT: ${{ secrets.PLAYGROUND_PAT }}
        with:
          cmd: "apps"
```

The above code will list all the apps deployed on the playground. You can specify which command to run inside the `Execute playground <command>` and it will run that command on each push to the repository.

### Catalog Deploy Action

The next action is `catalog-deploy` action with which in each push you will be able to deploy a catalog to your napptive playground.

Create a new file named `catalog-deploy.yml` inside the `workflows` directory and paste this code inside it.
```
name: Deploy to Napptive Playground from Catalog
on: [push]
jobs:
  deploy:
    name: Catalog deploy
    runs-on: ubuntu-latest
    steps:
      # Deploying napptive/drawio:14.3.0 from the catalog
      - uses: napptive-actions/catalog-deploy-action@v4.1.0
        env:
          PLAYGROUND_PAT: ${{ secrets.PLAYGROUND_PAT }}
        with:
          appName: "napptive/drawio:14.3.0"
```
The above code will deploy the  `draw.io` app to your playground whenever you push any changes.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1665297065953/fW1QgHIrH.png align="left")

As you can see the app has been successfully deployed on my playground. You can also specify any type of app inside the `appName` property.

## Wrapping up !!!

I hope that the above 2 mentioned actions will be helpful to your while working with **Napptive**. I will write more blogs in the upcoming actions so that you'll get a better understanding of how to automate your whole playground. If you have any doubts related to DevOps and Flutter, feel free to reach me out on **[Twitter](https://twitter.com/Hasnain_Makada)** and **[Showwcase](https://showwcase.com/hasnainmakada-99)**.

Happy Coding :)