---
title: "A Guide to Understanding the ADD and COPY Commands in Dockerfile"
seoTitle: "A Guide to Understanding the ADD and COPY Commands in Dockerfile"
seoDescription: "Preserving Directory Structure in Docker Images with COPY and ADD Commands: A Deep Dive into Dockerfile Configuration."
datePublished: Sat Jul 29 2023 10:13:38 GMT+0000 (Coordinated Universal Time)
cuid: clknuubrd000909le5zjj2bs2
slug: a-guide-to-understanding-the-add-and-copy-commands-in-dockerfile
canonical: https://www.showwcase.com/show/34759/a-guide-to-understanding-the-add-and-copy-commands-in-dockerfile
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690624991397/2830cc7f-9aaf-41ab-8ab9-bf9cc3866af9.png
tags: docker, nodejs, devops, dockerfile, directory-structure

---

# Introduction

Hey everyone, I am Hasnain Makada, and I am currently working as a Rotational Super Writer at [Showwcase](https://showwcase.com/) where I produce high-quality content on tech and make it understandable in a simple for my community. Today in this blog, we are going to see how the **COPY** and **ADD** commands work in the Dockerfile as well as how to preserve your directory structure inside your docker images.

So, without wasting any furthermore time, Let's get started 🔥

# What is a Dockerfile?

Docker is a popular platform for building, shipping, and running applications in containers. It allows developers to package their applications and dependencies into a single unit called a container, which can then be easily deployed and run on any system that supports Docker.

A Dockerfile is a script that contains a set of instructions for building a Docker image. It specifies the environment and dependencies needed to run an application inside a container. A Dockerfile contains commands that tell Docker how to build a Docker image, including how to install dependencies, copy files, and set up the environment.

When you run the `docker build` command, Docker reads the instructions in the Dockerfile and creates a Docker image based on those instructions. The Docker image is a snapshot of the environment and dependencies needed to run an application. This image can then be used to create Docker containers, which can be run on any system that supports Docker.

In summary, a Dockerfile is a powerful tool for building custom Docker images tailored to your specific application and environment requirements. It allows for a more efficient and consistent way of packaging and deploying applications in a containerized environment.

# What does a typical Dockerfile look like?

A Dockerfile is a simple text file that contains a series of instructions for building a Docker image of your application. You can create a Dockerfile in your application's root directory, which will specify how to package your application into a Docker image. It's important to note that the Dockerfile should not have any file extensions, and you should follow the recommended naming conventions for your Dockerfile.

Here's the demo of a dockerfile converting a Node JS app to a docker image.

```javascript
FROM node:latest

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

ENV PORT=3000

EXPOSE 3000

CMD [ "node", "app.js" ]
```

This file will convert your Node JS app to a docker image which you can ship it anywhere in your cloud provider.

# The COPY and ADD Command in a Dockerfile

Now let's jump on to the main point of this blog, what does the COPY and ADD command do in your Dockerfile and also see how to use them to preserve the directory structure of your app.

## Using Docker COPY to copy folders and files and keeping the directory structure.

The syntax of the COPY command is as follows,

```javascript
COPY <source> <destination>
```

The COPY command in Dockerfile is used to copy files or directories from the host machine to the Docker image. It will first take the **source** directory from where all the files are located inside the host machine and the **destination** directory will specify where all the files should be copied inside the **Docker image**.

For example, suppose we have a directory structure like this,

```javascript
my-app/
├── src/
│   ├── index.js
│   └── utils/
│       └── helpers.js
└── package.json
```

Now we want to copy the `my-app` directory inside the `/app` directory inside the docker image. Now we can achieve this while preserving the directory structure by using the following command.

```javascript
COPY my-app /app/my-app
```

The directory tree will look like this in our case,

```javascript
app/
	|-- my-app/
						|-- Dockerfile
						|-- app.js
						|-- index.html
						|-- node_modules
						|-- package-lock.json
						|-- package.json
```

Our source code is going to be included inside the my-app directory as shown in the above tree.

The above command will **COPY** the `my-app` source directory from the host machine inside the `/app/my-app` directory inside the docker image.

## Using Docker COPY to copy the files to a container without keeping the directory structure

From the above example we have seen that the **COPY** command which we used will preserve the directory structure, now what if we don't want to preserve it. Let's see the example.

```javascript
COPY ./app /user/source/app
```

In this example, the `COPY` command is copying the entire `./app` directory from the host into the `/usr/src/app` directory in the container. However, because the destination directory is explicitly specified, any subdirectories within `./app` will be flattened into a single directory in the container, rather than being preserved as separate subdirectories.

So if the directory structure looks like this inside the host machine

```javascript
./app
├── public
│   ├── index.html
│   └── styles.css
├── src
│   ├── index.js
│   └── utils.js
└── package.json
```

Then after the `COPY` command, the `/usr/src/app` directory in the container would have the following contents:

```javascript
/usr/src/app
├── index.html
├── index.js
├── package.json
├── styles.css
└── utils.js
```

As you can see, the `public` and `src` subdirectories have been flattened into a single directory within the container.

## ADD Command

The syntax of the ADD command is as follows,

```javascript
ADD <source> <destination>
```

The **source** is the path to the file or directory which is located inside the host machine or a remote URL and the **destination** is the path where the file or directory should be added inside the Docker image.

To preserve the directory structure when using the ADD command, we can follow the same approach as we did with the COPY command. For example, to add the`my-app` directory to the `/app` directory inside the Docker image while preserving the directory structure, we can use the following ADD command:

```javascript
ADD my-app /app/my-app
```

This will add the `my-app` directory from the host machine to the `/app/my-app` directory inside the Docker image, preserving the directory structure.

# Let's see it practically

Now that we have discussed the **COPY** and the **ADD** command, let's create a Node JS hello-world app and test it and see how it creates a directory tree inside the Docker image.

You can directly create a clone of the Node JS app in your system,

%[https://github.com/hasnainmakada-99/hello-world-app] 

Here's the Docker script to create the Docker image of the app,

```javascript
FROM node:latest

WORKDIR /app/my-app

COPY package*.json ./

RUN npm install

# Add application files to the container (Just an Example)
# ADD https://github.com/example/my-app/archive/master.tar.gz ./

COPY . /app/my-app

ENV PORT=3000

EXPOSE 3000

CMD [ "node", "app.js" ]
```

Now here's the explanation of what the dockerfile does,

1. `FROM node:latest`: This line specifies the base image to use for the container. In this case, it uses the latest version of the official Node.js image from Docker Hub.
    
2. `WORKDIR /app/my-app`: This line sets the working directory for the container to `/app/my-app`.
    
3. `COPY package*.json ./`: This line copies the package.json and package-lock.json files from the host machine to the container's working directory.
    
4. `RUN npm install`: This line runs the `npm install` command inside the container to install the dependencies listed in the package.json file.
    
5. `COPY . /app/my-app`: This line copies the rest of the application files from the host machine to the container's working directory.
    
6. `ENV PORT=3000`: This line sets an environment variable named `PORT` to the value of `3000`.
    
7. `EXPOSE 3000`: This line exposes port `3000` on the container.
    
8. `CMD [ "node", "app.js" ]`: This line specifies the command that should be run when the container starts. In this case, it runs the `node` command with `app.js` as its argument.
    

Now build the image by running `docker build -t node-app node-app .`

It will take some time to build the image, after it is built successfully run the below command 👇

```javascript
docker run -d --name node-app node-app
```

and your web app will start running at [http://localhost:3000](http://localhost:3000) 👇

![img](https://project-assets.showwcase.com/700x/12496/1682089959646-image.png?type=webp align="center")

Now open the running container of your image inside docker and go to terminal 👇

![img](https://project-assets.showwcase.com/700x/12496/1682090026320-image.png?type=webp align="center")

Install the necessary packages to view the directory tree inside the docker container

```javascript
apt-get update && apt-get install -y tree
```

After the above package has been installed, run `tree /app/my-app` inside the container terminal.

![img](https://project-assets.showwcase.com/700x/12496/1682090187944-image.png?type=webp align="center")

As you can see from the above image, our directory structure has remained as it was defined by us.

# FAQ's

1. **When the docker images are in container mode, which OS's kernel is used inside the container?**
    

Docker images run inside a container that uses the host operating system's kernel, which is typically a Linux kernel. This means that when you run a Docker container on a Windows or macOS host, the Docker container is still using a Linux kernel.

1. **Which package is used in Linux to see the directory tree?**
    

The `tree` package is used to see the directory structure in a tree like format inside the Linux kernel, it is simple to install, just run `apt-get install -y tree` and it will get installed successfully.

1. **What is the purpose of a Dockerfile?**
    

A Dockerfile is a file used to build Docker images by specifying the steps required to set up an application's environment. It automates the process of building a Docker image, making it easier to deploy applications consistently and reproducibly across different environments.

1. **What does the** `docker build` **command do?**
    

The `docker build` command builds a Docker image from a Dockerfile by executing the instructions specified in the file. It packages an application and its dependencies into a single image that can be used to run the application in a Docker container.

1. **What does the** `docker run` **command do?**
    

The `docker run` command is used to start a Docker container from a Docker image. It creates an instance of the image and runs it as a separate process on the host system. You can specify options such as port mappings, environment variables, and volume mounts to configure the container's behavior. Once the container is running, you can interact with it using the command-line or other tools.

# Conclusion

In conclusion, the COPY and ADD commands in Dockerfile are essential for adding files or directories to a Docker image. To preserve the directory structure when using these commands, we need to ensure that the `<destination>` path includes the correct directory structure. By following the examples and best practices provided in this blog post, readers can use these commands effectively in their own Docker projects. If you have any further queries related to DevOps and Flutter, feel free to reach out on [Twitter](https://twitter.com/Hasnain_Makada) and [Showwcase](https://showwcase.com/hasnainmakada-99)

Happy Coding 😃