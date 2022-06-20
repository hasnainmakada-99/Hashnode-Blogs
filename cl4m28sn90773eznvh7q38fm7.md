## Introduction to Datree and prevent Kubernetes misconfiguration from reaching production using Datree

### Introduction

Hey everyone in this blog I'm gonna talk about what is Datree and how Datree prevents your Kubernetes misconfigurations from reaching your production environment. You may be confused what is production enviroment ? so let me break it down for you,

There are mainly 2 types of environments are there when you are developing something, It can be anything website, application etc. Development & Production environment, In the development environment you develop the application from scratch and when the application is working perfectly you push it towards the production environment, The production environment is used to deploy the application or website you designed to the end user who is going to use it.

Now that you know the difference between development & production let's move forward:

### What is Datree ?

Datree is a tool which is used to prevent Kubernetes misconfiguration and it provides developers a simplified Kubernetes deployment experience so they don't need to remember so many rules governing development

Datree is a CLI (Command Line Interface) tool that supports the Kubernetes owners by preventing developers to make mistake in the Kubernetes configurations which can cause clusters to fail in production.

### How it prevents misconfigurations ?

When you are working with Kubernetes there are chances that when you create a pod, sometimes we make mistake in the YAML file, whether it can be indentation mistake or a version tag is not there etc. So Datree analyzes your whole file which you have given to it and it has a set of policies and rules with which it validates your file. If your file follows the rules and policies of Datree then you're good to go otherwise it will tell you to improvise your file.

### Steps to install Datree

The following steps helps you to install Datree in your local system, make sure that your docker desktop is up and running on your system

#### For windows

- Open PowerShell and run it as administrator

- Then paste this command into it 

```
iwr -useb https://get.datree.io/windows_install.ps1 | iex

```
- After it will take some time to install
- After it has been installed close and open your PowerShell again and run the `datree` command in it

- It will show you the output as below:
![datree install.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1655202571960/V5b8Iac1a.png align="left")

- You have successfully set up Datree on your machine

For Linux and mac users make sure to check out this [link](https://hub.datree.io/#1-install-the-datree-cli)

### Usage using Datree's demo configuration file

Now we've installed Datree it provides us a demo configuration which we can use to test it. Datree also provides us a dashboard in which we can see the history that how many tests were conducted on our machine and we can also see the policies which datree uses while performing these tests.

You can sign into [Datree](https://datree.io/) and after installing it, it will be integrated automatically with your host machine with the access token provided to your machine.

The dashboard will look like this after logging in,

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1655387419288/eKDfKfi8J.png align="left")

I've enabled all the policies on mine, but by default only 30 or 21 policies will be enabled.

Let's get started with Datree

- Open your terminal and create a new folder on your desktop or drive using the `mkdir <folder-name>`
- Navigate to the created folder using the `cd <folder-name>`
- And execute this command on your terminal `datree test ~/.datree/k8s-demo.yaml`

After executing this command it will perform the tests on the k8s-demo.yaml file and the outputs will be as follows,

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1655388368773/PjrQFdZ1_.png align="left")

It will also show us a summary table in which it will tell us how many many tests were successful and how many were failed

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1655388437145/wXjrU_TX0.png align="left")

The Datree CLI perform 3 types of tests, YAML validation, Kubernetes validation and the policy checks which you've provided. Lets discuss each and every test which Datree performs.

#### YAML validation

The first test which the Datree CLI performs is the YAML validation check. It checks the syntax and indentation of the YAML file and makes sure that it is a valid YAML file

For more information [refer](https://hub.datree.io/welcome/how-datree-works#what-is-a-datree-policy-check).

#### Kubernetes schema validation

The second test which Datree performs is the Kubernetes schema validation. It performs the checks on the YAML files and ensures that it is a valid Kubernetes manifest file

This check is performed by the [kubeconform](https://github.com/yannh/kubeconform) tool which is built in with Datree.

#### Policy checks

The third check which Datree performs are the policy check which are defined by default in Datree, you can check them out in the Datree dashboard.

Datree provides so many inbuilt policies by default and you can enable or disable them and you can also specify custom error messages on the policy checks

If you want to understand about any policy, you can click on the `i` button here,

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1655389845606/3x7-09Y4w.png align="left")

### Creating our own policy

If you want to create your own policy in Datree for testing you create it in Datree dashboard. Click on the create policy button on the left and assign name to your policy and click on the check button, and that's it you own custom policy has been created.


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1655390363820/otdqCS-NS.png align="left")

After creating your custom policy you can decide which policies you want to keep in it and which to not by enabling or disabling them.

### Changing policies using the YAML policy file

In Datree we can also customize our custom policies using YAML policy file which we can download from our Datree dashboard. Inside the policy file we can specify the policies the policies which we want to add in our own custom policy.

For downloading the policy file:
- Click on your profile in the Datree dashboard
- Then click on settings
- After clicking on the settings you will be redirected towards the setting page, Inside the setting page enable the `Policy as code` slider
- After enabling go back to your dashboard and you can see the `Export Policies` button.
- Click on the button and you can download your policies. It will download your all policies in a YAML file named as `policies.yaml`
- After downloading your policies open it in VS Code it will look something like this,
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1655439459926/SoLktnvB7.png align="left")

You can map your custom policies which you made using the name tag inside the policies file and inside the rules you can comment / uncomment any policy which you want and you can also define your custom failure messages inside the `policies.yaml` file.

### Publishing YAML file

After making changes in the `policies.yaml` file you can publish it directly to your Datree dashboard.

Steps to publish it:
- Open the folder in your terminal
- And type `datree publish policies.yaml` inside it
- And it will be published successfully to your Datree dashboard
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1655439862111/_TEKR01kO.png align="left")

- Check out your dashboard to see the changes.

> Note: If you want to make changes from the dashboard then you have to disable the 
 `Policy as code` slider from your settings

### Reference

For more reference regarding Datree you can check out it's official documentation [here](https://hub.datree.io/).

### Conclusion

I hope you now understood what is Datree and how it is used, If you have any further doubts related to it make sure to reach me out on [Twitter](https://twitter.com/Hasnain_Makada) and [Showwcase](https://Showwcase.com/hasnainmakada-99) 😊