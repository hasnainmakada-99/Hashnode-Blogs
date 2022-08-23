## How to deploy custom application on Napptive using Playground CLI

### Introduction

Hey everyone I am Hasnain Makada and I am currently working as a developer advocate at [napptive](https://napptive.com/) where I work closely with the platform continuously and explore new DevOps tools and technologies.

In this blog, I am going to teach you how you can deploy your first custom cloud-native app on Napptive. But before diving deep into that we are going to install the playground CLI & take a look at the pre-built applications which the Napptive catalogue already provides us and how we can deploy them.

### Understanding Playground (GUI)

Before installing the playground CLI, There is a GUI that Napptive already provides us if we want to work with apps. The GUI consists of almost every functionality so you can decide which is best for you.

To get access to the GUI go to https://playground.napptive.dev/ and sign in with your GitHub account to access the playground. By default, Napptive provides you with the free plan but you can also check out their paid plans via https://napptive.com/pricing

After successfully signing up, You'll be inside the GUI

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1660818340856/ePJwZejcd.png align="left")

Now you can configure your custom environments as per your use case
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1660818619615/ejmoApkfa.png align="left")

Now click on the catalogue button and it will show you a list of pre-built applications for your use case
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1660818691463/GPX4ZrJvH.png align="left")

Select any application and click on deploy, It will be deployed in just 10-20 seconds

After then you can see the application on your dashboard

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1660818821506/trXm0n8-H.png align="left")

### Installing playground CLI

To install the playground CLI on windows follow the official [docs](https://docs.napptive.com/Downloads.html#windows-releases)

### Interacting with the playground CLI

After installing the playground successfully, Type `playground` in the terminal to check whether it working correctly or not

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1660889522358/qH9EsZ9J1.png align="left")

Now login with your playground account to start interacting with it. Use `playground login`

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1660889618871/t7qUc3v-f.png align="left")

Now that you've logged into your default environment you can start using the playground commands. Firstly create a folder and redirect the terminal to your folder `cd <folder-name>`. Then get the `napptive-kubeconfig` file to connect to the cluster and deploy your custom applications `playground get-kubeconfig`

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1660889868636/k4K6p143B.png align="left")

You can get your current environment info using `playground env info`

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1660890005842/xPlBqASg7.png align="left")

To open your Napptive dashboard via CLI use `playground dashboard`

For more CLI commands visit the official [docs](https://docs.napptive.com/playground/CLI.html).

### Deploying Custom Application

Now that we're good to go, let's build a simple Nginx application and deploy it to our Napptive cluster. We're going to be dealing with YAML files for making our custom application, So if you don't know how to make YAML files checkout my [YAML Blog](https://hasnainm.hashnode.dev/intro-to-yaml)

Create a `custom-app.yaml` file inside your folder `touch custom-app.yaml`

Now open the YAML file inside the terminal or your favourite code editor (I generally prefer using CLI). `vi custom-app.yaml` and paste this code inside it.
```
apiVersion: core.oam.dev/v1beta1
kind: Application
metadata:
  name: custom-app
  annotations: # include optional annotations and/or labels.
    version: v1.0.0
    description: "Customized version of nginx"
spec:
  components:
    - name: nginx # an nginx component exposing port 80
      type: webservice
      properties:
        image: nginx:1.20.0
        ports:
        - port: 80
          expose: true
      traits:
      - type: napptive-ingress # a napptive-ingress trait to get a public endpoint
        properties:
          name: nginx
          port: 80
          path: /

```
The above code will create a simple application but a customized version of nginx.

To create and deploy it on Napptive run `playground apps create custom-app.yaml` and it will successfully create the application and deploy it. You can see it via the dashboard `playground dashboard`

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1660890885737/YMD1CvMnP.png align="left")

You can see it is deployed. Click on the app and go to the endpoint of it.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1660890935328/tKW5gn9js.png align="left")

And it's done. Congratulations 🎉🎉 on deploying your first custom application on Napptive

### Conclusion

I hope that now you learned how to deploy your custom apps on Napptive, So if you have any doubts regarding the platform feel free to reach out on [showwcase](https://showwcase.com/hasnainmakada-99) & [Twitter](https://twitter.com/Hasnain_Makada).

Goodbye 😊
