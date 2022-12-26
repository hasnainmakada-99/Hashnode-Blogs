# GitHub Actions to use for your next Open Source Project

# **Introduction**

**Hey everyone I am Hasnain Makada, currently working as a Developer Advocate at** [**Napptive**](https://napptive.com/) **where I explore the platform in-depth and educate the community regarding** [**DevOps**](https://aws.amazon.com/devops/what-is-devops/) **and** [**Flutter**](https://flutter.dev/)**. I also maintain an Open Source project where beginners can contribute to it and get their journey started with Open Source.**

You can check out my project by clicking [**Here**](https://github.com/hasnainmakada-99/Open-Source-With-Hasnain)

Apart from that I also write blogs related to DevOps and Flutter on [**Hashnode**](https://hasnainm.hashnode.dev/) & [**Showwcase**](https://hasnainmakada-99.showwcase.com/shows).

In this blog, I will talk about some of the most important GitHub actions you can integrate with your Open Source project and save you hours and hours of your time.

If you don’t know about GitHub and you’re reading this for the first time, make sure to check out my blog on [**Hashnode**](https://hasnainm.hashnode.dev/github-actions)

So without wasting any further time, let’s get started with the first action,

## **Greetings Action by EddieHub Community**

If you’ve started an Open Source project and you’d like beginners to contribute to it and make them feel like they’re a part of the community, there is an awesome action developed by the [**EddieHub Community**](https://github.com/EddieHubCommunity) that you can easily integrate with your project and you can edit the workflow as per your requirement and greet the user when they contribute to the project.

You can check out the GitHub-Action [**Here**](https://github.com/EddieHubCommunity/gh-action-community)

Here is a small example of my workflow from OSWH which I use to greet someone whenever they contribute anything to the community

```yaml
on:
  fork:
  push:
    branches: [main]
  issues:
    types: [opened]
  issue_comment:
    types: [created]
  pull_request_target:
    types: [opened]
  pull_request_review_comment:
    types: [created]

jobs:
  welcome:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v1
      - uses: EddieHubCommunity/gh-action-community/src/welcome@main
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }}
          issue-message: "<h3>Hey! contributor, thank you for opening an Issue 🎉.</h3>"
          pr-message: "<h3>Hey! contributor, thank you for opening a Pull Request 🎉.</h3>"
          footer: "Soon one of our maintainers will review it and provide you with feedback/suggestions. If you think it's something urgent, feel free to reach out <a href='https://twitter.com/Hasnain_Makada'>Hasnain Makada</a> on <b>Twitter</b>. Star ⭐ this repo to show us support.</b><br><br><b>Happy, Open Source!</b>"
```

In the above workflow, I’ve stated that whenever a contributor raises a PR or Issue, the workflow will greet them according to the issue message and PR message provided.

This action is useful to me and I use it in all my projects because I never know who will contribute to it, but they should be greeted once.

Now that we’ve discussed greetings action, Let’s move on to the next one,

## **IMGBOT - Optimize your Images**

In Open-Source projects, we often find it difficult to optimize images because that’s a difficult and time-consuming task and often requires some practice, but don’t worry there is an awesome tool for that also.

**IMGBOT** is an application that you can automatically integrate with your repository and the bot will automatically detect all the local images from your repository it will optimize them and raise a PR for the same.

Make sure to check it out 👉🏻 [**here**](https://imgbot.net/)

![https://avatars.githubusercontent.com/u/80986210?s=280&v=4](https://avatars.githubusercontent.com/u/80986210?s=280&v=4 align="center")

## **All Contributors - Recognize All Contributors**

Now that we are talking about open source, we must include all the contributors in our project and make them feel appreciated for contributing to open source.

All contributors bot is a GitHub application with which you can include the images of your contributors which redirects to their main portfolio. The bot is pretty simple to set up and you can get started with it in no time.

Check out their official [**documentation**](https://allcontributors.org/)

![https://repository-images.githubusercontent.com/164268911/8bf40400-4c33-11eb-9164-5618ea9805ba](https://repository-images.githubusercontent.com/164268911/8bf40400-4c33-11eb-9164-5618ea9805ba align="left")

## **Send a Tweet Action**

When maintaining an open-source project there is a certain need to check whether any updates are made to our project or not, Send a tweet action by ethomson is an awesome workflow integration with which you can integrate your Twitter bot account and it will automatically tweet all the new changes pushed to the project.

The workflow is easy to use and does not contain any complex code, here is a simple example

```yaml
name: Send a Tweet 🐦

on:
  push:
    branches:
      - main

jobs:
  Tweet:
    runs-on: ubuntu-latest
    steps:
      - uses: ethomson/send-tweet-action@v1
        with:
          status: "Hello World"
          consumer-key: ${{ secrets.TWITTER_CONSUMER_API_KEY }}
          consumer-secret: ${{ secrets.TWITTER_CONSUMER_API_SECRET }}
          access-token: ${{ secrets.TWITTER_ACCESS_TOKEN }}
          access-token-secret: ${{ secrets.TWITTER_ACCESS_TOKEN_SECRET }}
```

By implementing the above example our workflow will work successfully in our project and will notify us whenever any new pushes are made to our project, keep the status of your workflow according to the topic which you need it to push to Twitter.

## **Mergify - Faster and Safer code merge**

If your open-source project is at scale and you want to completely automate it, I will suggest you use mergify. Mergify is an all-in-one tool to automate various tasks in your project such as assigning issues, merging PRs, etc…

I’ve also written a blog on Mergify on how to use it and automate your workflow with it, make sure to check out on [**Hashode**](https://hasnainm.hashnode.dev/the-new-way-to-automate-your-github-repositories)

![https://mergify.com/lib_okTisfLmCuKjyNYm/3z8ie6ou21zm4hux.png?w=1200&h=630&fit=crop](https://mergify.com/lib_okTisfLmCuKjyNYm/3z8ie6ou21zm4hux.png?w=1200&h=630&fit=crop align="left")

# **Wrapping Up!!!**

Now its time to wrap up our blog I hope that you liked my blog and don’t forget to follow me on [**Twitter**](http://twitter.com/Hasnain_Makada) and [**Showwcase**](https://hasnainmakada-99.showwcase.com/) and feel free to reach me out also in-case of any doubts.