# How to build a CI/CD pipeline with Jenkins (explained with a project)

# Introduction

Hey everyone I am Hasnain Makada currently working as a Developer Advocate at [Napptive](https://napptive.com) where I explore the platform in-depth and also teach about DevOps and Flutter to the community as well via my blogs on [Hashnode](https://hashnode.com) & [Showwcase](https://showwcase.com/hasnainmakada-99).

In this blog, I am going to teach you how to build a CI/CD pipeline using Jenkins and the best part of this blog is, I am going to build the pipeline and use a project with it to explain how everything works practically.

# What is Jenkins?

[Jenkins](https://www.jenkins.io/) is an open-source automation server. It helps to automate the parts of software development related to building, testing and deploying, facilitating continuous integration and continuous delivery. With Jenkins, you can easily automate various tasks in your software such as testing the code periodically to detect any errors, building the app after testing, and so on...

With Jenkins, you mainly have to build a pipeline for your entire project and inside the pipeline, you can define various stages the CI/CD will go on. Jenkins is free software and is completely open source for everyone to contribute.

# Let's build the actual pipeline

Now that we've discussed Jenkins, let's get started building out the actual pipeline and see how it is useful in building our projects.

Before starting out make sure that you've installed Jenkins properly in your system, If you're new to Jenkins and don't know how to install it, check out the official documentation by [Jenkins](https://www.jenkins.io/doc/book/installing/).

Now go to your dashboard, and click on **New Item**

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1668608160160/jVnRaLCsr.png align="left")

Then enter the name of your item and select pipeline from the above list of projects. As we are creating a pipeline we are selecting that, otherwise, we can create a freestyle project also. But freestyle projects have their own disadvantages which you can check out [here](https://www.jenkins.io/doc/book/using/).

Name the pipeline as `CI-CD pipeline GitHub` and create it.

Moving on to the next, Jenkins will ask you to configure your project and will ask you several parameters such as a description, whether it is a GitHub project, etc... It will also ask you for triggers to build the project periodically and so on...

Here I am selecting to build the project periodically because that's the job of CI/CD, right?

Click on the `Build Periodically` and paste this inside the box `H/5 * * * *`. This will automatically build the project every 5 minutes to ensure that the pipeline is up-to-date.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1668687339222/c02Fg2m75.png align="left")

After then, go to the pipeline section and select pipeline from SCM. Select `GIT` as the SCM and enter the URL of your GitHub Repository.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1668687507490/VEZyu4Mzz.png align="left")

Now click on save and your pipeline is created successfully.

Now that our pipeline is successfully integrated with our project, we are going to create a sample hello world project in node js and ensure that our pipeline gets built every 5 minutes for us to perform certain node commands.

Create a Jenkinsfile inside the root folder of your project and paste this code inside it.

```plaintext
pipeline {
  agent any
  tools {nodejs "node"}
  stages {
    stage('Example') {
      steps {
        sh 'npm version'
      }
    }
  }
}
```

> Remember: To run Jenkins on node js projects, make sure you have the Node JS plugin installed on your machine, If you don't know how, check out [here](https://plugins.jenkins.io/nodejs/)

Add the file, commit and push the changes to the main repo.

Now that we've set the build to periodically, it will get started every 5 minutes, but we can do that by clicking on the **Build Now** button on the side panel.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1668688015013/JgjSej1WH.png align="left")

Head over to the main dashboard and you can see that we've successfully run our first pipeline in our repository

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1668688262408/HCobUYMy-.png align="left")

Similarly define more steps and create more stages and the pipeline will build every 5 minutes. I've used the declarative approach in defining the pipeline of Jenkins, but you can use the scripting syntax too. For more info about pipeline syntax, check out [here](https://www.jenkins.io/doc/book/pipeline/)

# Wrapping up!!!

Alright, everyone, this was just the demo of Jenkins on how to create a pipeline and integrate it with GitHub, So if you wanna learn more about Jenkins, Check out their official [documentation](https://www.jenkins.io/doc/book/getting-started/).

I hope that by now you have got the Idea of what is CI/CD and how Jenkins implements the concept of CI/CD by providing such simplicity. If you have any further doubts related to DevOps and Flutter, reach out to me on [Twitter](https://twitter.com/Hasnain_Makada) and [Showwcase](https://Showwcase.com/hasnainmakada-99).

Till then Happy Coding 😀😀😀