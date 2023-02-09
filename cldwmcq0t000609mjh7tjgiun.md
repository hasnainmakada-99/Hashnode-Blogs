# Convert a flutter web app to a docker container

# Introduction

Hey everyone I am hasnain makada, currently building out [**"Open source with Hasnain"**](https://github.com/hasnainmakada-99/Open-Source-With-Hasnain)**,** where every beginner can get their journey started by contributing to open source and they can find tons of resources related to their specific tech stack. I also write blogs on Hashnode and showwcase where I teach about various DevOps and Flutter concepts.

In this blog I am going to teach you about how you can covert your flutter web app, to a docker container and make it run on the web without installing all the flutter dependencies, So without any further ado let's get started,

# Creating the Dockerfile

Open your terminal and create the flutter app by running `flutter create flutter_docker_app`. Wait for some time and the app will be created successfully. For this blog, we are going to use the simple counter app which is pre-provided by flutter.

Now create a docker file inside your app and make sure the naming convention is `Dockerfile`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1675843601965/5e12fba5-815d-4363-9419-4628064db224.png align="center")

Now paste this Docker code inside the docker file,

```apache
# Stage 1
FROM debian:latest AS build-env

RUN apt-get update 
RUN apt-get install -y curl git wget unzip libgconf-2-4 gdb libstdc++6 libglu1-mesa fonts-droid-fallback lib32stdc++6 python3
RUN apt-get clean

RUN git clone https://github.com/flutter/flutter.git /usr/local/flutter

ENV PATH="/usr/local/flutter/bin:/usr/local/flutter/bin/cache/dart-sdk/bin:${PATH}"

RUN flutter doctor -v

RUN flutter channel master
RUN flutter upgrade
RUN flutter config --enable-web

RUN mkdir /app/
COPY . /app/
WORKDIR /app/
RUN flutter build web

# Stage 2
FROM nginx:1.21.1-alpine
COPY --from=build-env /app/build/web /usr/share/nginx/html
```

Now let's understand the above docker code step-by-step,

1. The first line defines the base image to be used for the first stage of the build process: `"FROM debian:latest AS build-env"`. This specifies that the latest version of the Debian operating system image will be used as the base image for the first stage, and the stage is named "build-env".
    
2. Next, the necessary dependencies for Flutter are installed using apt-get. The commands `"RUN apt-get update"` and `"RUN apt-get install"` install the following packages: curl, git, wget, unzip, libgconf-2-4, gdb, libstdc++6, libglu1-mesa, fonts-droid-fallback, lib32stdc++6, and python3.
    
3. The Flutter repository is then cloned using the command `"RUN git clone` [`https://github.com/flutter/flutter.git`](https://github.com/flutter/flutter.git) `/usr/local/flutter"`.
    
4. The environment variable PATH is then set to include the Flutter binary and Dart SDK binary in the PATH using the command `"ENV PATH="/usr/local/flutter/bin:/usr/local/flutter/bin/cache/dart-sdk/bin:${PATH}""`.
    
5. The Flutter doctor is run to check the Flutter installation using the command `"RUN flutter doctor -v"`.
    
6. The Flutter web is enabled using the commands `"RUN flutter channel master"`, `"RUN flutter upgrade", and "RUN flutter config --enable-web"`.
    
7. The application files are copied into the container using the commands `"RUN mkdir /app/"` and `"COPY . /app/"`. The working directory is set to `"/app/"` using the command `"WORKDIR /app/"`
    
8. The Flutter build web command is run to build the application using the command `"RUN flutter build web"`.
    
9. The second stage of the build process starts with the line `"FROM nginx:1.21.1-alpine"`. This specifies that the latest version of the Nginx operating system image will be used as the base image for the final runtime image.
    
10. The final runtime image takes the build output from the previous stage and copies it to the default Nginx webroot directory using the command `"COPY --from=build-env /app/build/web /usr/share/nginx/html"`.
    

# Building the docker image

Now build the docker image by running `docker build -t myflutterapp .` and wait for some time to build the image.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1675845159564/af7572f4-73d6-4c5f-bce8-7f0c8adc42d8.png align="center")

After the image has been built successfully, you can see it inside your docker desktop app.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1675845418423/f42473bc-1a13-403b-a3c5-4d5ae125a059.png align="center")

Now that our docker image has been created successfully, So let's move on to the next part,

# Running the docker image

To run the docker image as a container, Run `docker build -d -p 1200:80 --name myflutterapp myflutterapp` . This command will run the docker image in the detachable mode and we've also specified the port number to 1200 from 8080 and we've given a name to our container as well.

![](https://media.giphy.com/media/nWoopautvgcETcMY4A/giphy.gif align="center")

# Conclusion

I hope that by now you must've got the idea of how to run a flutter app inside docker. If you have any doubts related to DevOps and Flutter, feel free to reach out at [**Twitter**](https://twitter.com/Hasnain_Makada) and [**Showwcase**](https://showwcase.com/hasnainmakada-99)**.**

Till then, Happy Coding 😄😄😄