---
title: "Host a Web App on Microsoft Azure using Azure Container Registry"
seoTitle: "Host a Web App on Microsoft Azure using Azure Container Registry"
seoDescription: "In this article, I'm going to show how to host a web app on MS Azure with the help of Azure Container Registry."
datePublished: Sun Apr 09 2023 01:30:39 GMT+0000 (Coordinated Universal Time)
cuid: clg8qa7l0008gu7nvd0a53rjp
slug: host-a-web-app-on-microsoft-azure-using-azure-container-registry
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1680590929206/04f64f6e-e3ae-48bd-bd8f-4393adb18a98.png
tags: docker, azure, nodejs

---

# Introduction

Hey everyone, I am Hasnain Makada and I am currently building out "[***Open Source with Hasnain***](https://hasnainmakada-99.github.io/Open-Source-With-Hasnain/#/)" where I encourage every beginner to contribute to open source and network with like-minded folks. I am also a quality crew at [Showwcase](https://showwcase.com) and a beta ambassador at the Microsoft Learn Student Ambassador program where I host several events and upskill my community by providing various resources.

Today, in this blog I am going to show you how to host a web app on Azure with the help of Azure Container Registry. We're going to build the Web App, create the docker image out of it, upload it to ACR and then create a web app out of it.

So without wasting any further time, let's get started.

# What is Microsoft Azure?

Microsoft Azure is a cloud computing platform that provides a wide range of services and tools for businesses and individuals to build, deploy, and manage applications and services on the Internet. It allows users to store, process, and analyze data in the cloud, rather than on their physical servers or computers.

Azure offers a variety of services including virtual machines, databases, storage, machine learning, and many more. Users can use these services to create and run applications, host websites, store and retrieve data and manage their infrastructure.

In simpler terms, Microsoft Azure is like renting a computer or server on the internet that allows you to store and process data, run applications, and perform other computing tasks without having to physically own and maintain the hardware.

For this blog purpose, you'll need an Azure account which you can create from [here](https://azure.microsoft.com/en-in/get-started/azure-portal/).

# What is Azure Container Registry?

Azure Container Registry is a managed, private registry service provided by Microsoft Azure for storing and managing container images used in container-based applications.

In simple terms, containerization allows developers to package their applications and all their dependencies into a single, portable image. These images can then be stored in a container registry like Azure Container Registry, which acts as a centralized repository for these images.

Azure Container Registry allows you to store and manage container images securely and at scale. You can use it to create, store, manage, and deploy Docker container images to Azure Kubernetes Service (AKS) or other container platforms. It provides features such as geo-replication, lifecycle management, and access control to help you manage your container images and ensure their availability and security.

Using Azure Container Registry can help simplify and streamline the deployment and management of container-based applications by providing a centralized and secure location for storing and distributing container images.

# Creating the Azure Container Registry

For this blog, we're going to host our docker image on ACR, So let's start creating it.

1. Go to the Azure [portal](https://portal.azure.com/) and click on `Container registries`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680697140454/6d2a001d-0e3c-49e0-ba86-af80c1cd85aa.png align="center")
    
2. Click on **Create**
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680697293559/9c1aec51-cd3f-4f96-9392-9032011d2f77.png align="center")
    
3. Now fill in the details as follow,
    

<table><tbody><tr><td colspan="1" rowspan="1"><p><strong>Resource group</strong></p></td><td colspan="1" rowspan="1"><p>click on <code>create new</code> and give a name to your resource</p></td></tr><tr><td colspan="1" rowspan="1"><p><strong>Registry name</strong></p></td><td colspan="1" rowspan="1"><p>give a unique name to your ACR</p></td></tr><tr><td colspan="1" rowspan="1"><p><strong>Location</strong></p></td><td colspan="1" rowspan="1"><p>East US</p></td></tr><tr><td colspan="1" rowspan="1"><p><strong>SKU</strong></p></td><td colspan="1" rowspan="1"><p>Standard</p></td></tr></tbody></table>

Now click on review + create and review all the details which you filled in and click on create.

Wait for some time and your ACR will be created successfully.

## Creating the web app on your local system

For hosting purposes, we're gonna create a hello world web app using Express JS and Node JS

* Create a new folder and run `npm run init -y` on your terminal inside the folder
    
* Install the Express JS node module by running `npm i express`
    

Create 2 files, one is index.html and another is app.js and paste the code from the below gists

**Index.html**:

[https://gist.github.com/hasnainmakada-99/1851dd29347c72a6e9eb25eb0d3701c7](https://gist.github.com/hasnainmakada-99/1851dd29347c72a6e9eb25eb0d3701c7)

**app.js:**

[https://gist.github.com/hasnainmakada-99/1aa89b6266feaa675839e40994b2cf74](https://gist.github.com/hasnainmakada-99/1aa89b6266feaa675839e40994b2cf74)

And your web app is ready to be hosted

## Creating the docker image

Now that our app is ready to host on Azure, we first need to create a Docker image of our project and for that, you can copy this gist and paste it inside your `Dockerfile`

[https://gist.github.com/hasnainmakada-99/7f9b7bcec51fb4f2fa4dd0151a445ecc](https://gist.github.com/hasnainmakada-99/7f9b7bcec51fb4f2fa4dd0151a445ecc)

Build the image using `docker build -t hello-world .` and your image will be created successfully. You can view your image inside the docker desktop app.

# Moving to Azure Container Registry

Now that our docker image has been created successfully. Now it's time to move our docker image to the Azure container registry.

Now go to your container registry and go to the access keys and note down all the details on a notepad,

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680866956058/fea07b7d-48a1-4ce2-a5ef-19d650b44107.png align="center")

After then open your terminal and log in to your container registry with the **login server** credential.

```apache
docker login <your-login-server-credential>
```

It will then ask you for your username and password, just provide it from the access keys tab and your login will be successful.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680867269712/9d29b6bb-e2be-4737-b448-21716ccbecd2.png align="center")

Now tag your current image with your **login server** credential and push it to your ACR,

```apache
docker tag hasnainmakada/hello-world hasnainswebapp.azurecr.io/hello-world

docker push hasnainswebapp.azurecr.io/hello-world
```

If you've done all the steps correctly, your image has been pushed to your ACR successfully.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680868223888/6a9e965f-51db-49a9-8f52-58ae2aade501.png align="center")

# Creating the web app on Azure

Now that we've discussed Azure and ACR, Let's get started creating the Azure Web app

1. Go to the Azure Portal and click on `create a resource`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680592892104/06d16941-db23-4229-8c98-867a90517506.png align="center")
    

After Clicking on the create resource button, you'll be redirected to the second screen of the Azure web app.

1. Now go to the web app and click on `create`
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680593126137/eef51f1a-09f8-4fdb-9b1b-672484b1f2bd.png align="center")

It will ask you for basic details such as subscription, name, publish, runtime stack etc...

Fill in the details as follows,

<table><tbody><tr><td colspan="1" rowspan="1" colwidth="194"><p><strong>Subscription</strong></p></td><td colspan="1" rowspan="1"><p>Select your preferred subscription</p></td></tr><tr><td colspan="1" rowspan="1" colwidth="194"><p><strong>Resource group</strong></p></td><td colspan="1" rowspan="1"><p>Select the existing resource group which you created when creating ACR</p></td></tr><tr><td colspan="1" rowspan="1" colwidth="194"><p><strong>Name</strong></p></td><td colspan="1" rowspan="1"><p>Give a unique name to your web app</p></td></tr><tr><td colspan="1" rowspan="1" colwidth="194"><p><strong>Publish</strong></p></td><td colspan="1" rowspan="1"><p>select Docker Container</p></td></tr><tr><td colspan="1" rowspan="1" colwidth="194"><p><strong>Operating System</strong></p></td><td colspan="1" rowspan="1"><p>Linux</p></td></tr><tr><td colspan="1" rowspan="1" colwidth="194"><p><strong>Region</strong></p></td><td colspan="1" rowspan="1"><p>East US</p></td></tr></tbody></table>

Rest keep all the details as it is and click on `Next: Docker >`.

<table><tbody><tr><td colspan="1" rowspan="1" colwidth="143"><p><strong>Options</strong></p></td><td colspan="1" rowspan="1"><p>Single Container</p></td></tr><tr><td colspan="1" rowspan="1" colwidth="143"><p><strong>Image Source</strong></p></td><td colspan="1" rowspan="1"><p>Azure Container Registry</p></td></tr></tbody></table>

And the rest of the details it will fetch automatically from the ACR such as image name, tag, registry etc...

Then click on `Review + Create` and review all the details and click on **Create** and it will start creating your web app.

After then Go to your web app resource and click on the default domain URL

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680868694819/ae5681fe-c270-483d-9785-f34224d04a61.png align="center")

Wait for 1-2 mins and you're good to go, now your docker container is successfully hosted on the cloud.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680868971179/46ef59aa-7004-4d9d-ae51-974ae241e5a4.png align="center")

# Wrapping Up!!!

We learnt about Azure and ACR and also saw how to host a docker image to ACR and how to integrate the Azure web app with ACR. If you have any doubts related to DevOps and Flutter, feel free to reach out on [Twitter](https://twittter.com/Hasnain_Makada) and [Showwcase](https://showwcase.com/hasnainmakada-99).

Happy Coding 😀