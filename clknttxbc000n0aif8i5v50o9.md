---
title: "Azure Container Registry CI/CD workflow with Github Actions"
seoTitle: "Azure Container Registry CI/CD workflow with Github Actions"
seoDescription: "In this blog, I am going to teach you how you can set up a GitHub Actions workflow inside Azure Container Registry and deploy directly from GitHub."
datePublished: Sat Jul 29 2023 09:45:19 GMT+0000 (Coordinated Universal Time)
cuid: clknttxbc000n0aif8i5v50o9
slug: azure-container-registry-cicd-workflow-with-github-actions
canonical: https://www.showwcase.com/show/34728/azure-container-registry-cicd-workflow-with-github-actions
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690623605079/8dabf006-63b6-46b6-b31f-3df991d573e8.png
tags: github, azure, devops, ci-cd, github-actions-1

---

# Introduction

Hey everyone, I am Hasnain Makada currently working as a Rotational Super Writer at Showwcase where I create content on tech and explore new technologies and teach everyone. In this blog, I am going to teach you how you can set up a GitHub Actions workflow inside your Azure Container registry which will help you deploy your application directly from GitHub to ACR.

For this blog purpose, you'll need an Azure account which you can create from [here](https://azure.microsoft.com/en-in/get-started/azure-portal/).

So without wasting any furthermore time, Let's get started

# What are we going to push?

The main thing which this blog teaches us is to build our application which is already there on GitHub and with the help of GitHub Actions, build the docker image of it and push it to the ACR. Yes, it's that simple.

The docker image which we will build will take care of all the dependencies and packages, bundle them together and push it inside ACR

The GitHub Actions workflow will take care of all the things and will save us time deploying the application manually on Azure.

# Creating the sample web application and moving to Azure Container Registry

To Create the sample web application, please take all the following steps defined in this blog,

%[https://www.showwcase.com/show/34483/host-a-web-app-on-microsoft-azure-using-azure-container-registry] 

And your application and docker file will be created successfully.

Now create the Azure container registry as defined in the above link and push your docker image to your following ACR.

# Setting up the workflow and testing our app

Now push the application code which you created to GitHub, or you can also create a copy from the below link

%[https://github.com/hasnainmakada-99/hello-world-app] 

Now create a `.github` directory of your project and inside that create a `workflows` directory.

Now create a `acr_deploy.yaml` workflow inside the workflow directory which will rebuild our project using the Dockerfile which we provided and it will push it to the ACR.

Paste this code inside the `acr_deploy.yaml` file

## GitHub Actions Script for Azure Container Registry

```javascript
name: Build and Deploy to ACR

on:
  push:
    branches:
      - main

env:
  IMAGE_NAME: my-app
  REGISTRY_NAME: my-acr.azurecr.io
  REGISTRY_USERNAME: ${{ secrets.REGISTRY_USERNAME }}
  REGISTRY_PASSWORD: ${{ secrets.REGISTRY_PASSWORD }}

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Login to ACR
        uses: azure/docker-login@v1
        with:
          login-server: ${{ env.REGISTRY_NAME }}
          username: ${{ env.REGISTRY_USERNAME }}
          password: ${{ env.REGISTRY_PASSWORD }}

      - name: Build Docker image
        run: docker build -t ${{ env.IMAGE_NAME }} .

      - name: Tag Docker image
        run: docker tag ${{ env.IMAGE_NAME }} ${{ env.REGISTRY_NAME }}/${{ env.IMAGE_NAME }}:${{ github.sha }}

      - name: Push Docker image to ACR
        run: docker push ${{ env.REGISTRY_NAME }}/${{ env.IMAGE_NAME }}:${{ github.sha }}
```

This workflow will trigger a push to the `main` branch, and will perform the following steps:

1. Check out the code from the repository.
    
2. Log in to the Azure Container Registry using the credentials stored in GitHub Secrets.
    
3. Build the Docker image using the Dockerfile in the root of the repository.
    
4. Tag the Docker image with the commit SHA and the registry name.
    
5. Push the Docker image to the Azure Container Registry.
    

Note that this workflow assumes that you have already created an Azure Container Registry and have set up the appropriate credentials in GitHub Secrets. You will need to update the `REGISTRY_NAME`, `REGISTRY_USERNAME`, and `REGISTRY_PASSWORD` environment variables to match your own ACR configuration.

You can take all the credentials from the access keys tab inside Azure,

![img](https://project-assets.showwcase.com/700x/12496/1681905440970-image.png?type=webp align="left")

# Creating the web app from the ACR

Now that we've set up the ACR successfully you can now create your own web app from the ACR,

To create your web app from ACR, click on the link below

%[https://www.showwcase.com/show/34483/host-a-web-app-on-microsoft-azure-using-azure-container-registry] 

After creating your web app successfully, let's test it. Commit the file into your GitHub repository and wait for 1 - 2 mins till the actions get successful.

![img](https://project-assets.showwcase.com/700x/12496/1681907744767-image.png?type=webp align="center")

Make sure to enable the pulling from ACR inside your web app in the deployment centre. If it isn't turned on then it will not fetch the latest docker image from the repository.

And the new code will be deployed successfully

![img](https://project-assets.showwcase.com/700x/12496/1681909702277-image.png?type=webp align="left")

# Conclusion

Delete all the resources once you are done deploying your app otherwise Azure will start costing you for the resources. I hope that by now you must have understood how to set up CI/CD pipeline with the help of GitHub Actions in ACR and then push the new changes of ACR to Azure Web App. This was just the demo of it, you can do much more like integrating Azure k8s and replicating to multiple regions.

If you have any more doubts related to DevOps or Flutter, feel free to reach out on [Twitter](https:) and [Showwcase](https://showwcase.com/hasnainmakada-99)