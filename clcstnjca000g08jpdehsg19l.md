# My views about Appwrite🚀🚀🚀

# Introduction

Hey everyone I am Hasnain Makada, Currently building out [**Open Source with Hasnain**](https://github.com/hasnainmakada-99/Open-Source-With-Hasnain) where beginners can contribute to it and they can find various resources regarding their particular tech stack and get started with it. I also work as a Developer Advocate at [**Napptive**](https://napptive.com) where I explore the platform in Depth and I also educate the community about DevOps and Flutter.

In this blog, I am going to post my reviews about [**Appwrite**](https://appwrite.io/) which is an Open Source backend server that you can easily integrate with web, mobile, and Flutter also.

Before getting started with the main parts of appwrite, let's discuss what Appwrite is.

# What is Appwrite?

Appwrite is an open-source backend as a server providing all the necessary API(s) to build out any application developer wants.

The main aim of appwrite is to reduce the complexity of common and repetitive tasks to build modern apps. Appwrite provides you with a set of APIs, tools, and a management console UI to help you develop your apps a lot faster, and in a much more secure way.

Appwrite provides authentication and account management, user preferences, database and storage persistence, cloud functions, localization, image manipulation, and more.

You can install appwrite on any OS you use with just a single [**Docker**](https://www.docker.com/) command and it will be installed on your system. Appwrite is completely open-source in which you can contribute to it as well. Check out their [**GitHub Organization**](https://github.com/appwrite)**.**

# Appwrite Integration with Flutter

The integration of appwrite is pretty much straightforward with Flutter, I've not used it with any other SDK, but for flutter, I've found it pretty much easy. I use windows as my primary OS so I have to run one command in Docker.

```bash
docker run -it --rm `
    --volume /var/run/docker.sock:/var/run/docker.sock `
    --volume ${pwd}/appwrite:/usr/src/code/appwrite:rw `
    --entrypoint="install" `
    appwrite/appwrite:1.2.0
```

After running the above command, appwrite will ask you for some basic parameters such as setting the host address and so on... and it will get installed successfully

Appwrite will be available at the default port **80.**

For more info regarding the installation, you can check out their [official docs](https://appwrite.io/docs/getting-started-for-flutter).

After installing the appwrite, add one line inside the app-level `build.gradle` file and then your flutter app will be integrated with appwrite. Then init the SDK inside the `main.dart` file,

```bash
import 'package:appwrite/appwrite.dart';

Client client = Client()
    .setEndpoint('https://localhost/v1') // Your Appwrite Endpoint
    .setProject('5e8cf4f46b5e8')         // Your project ID
    .setSelfSigned(status: true);
```

After initiating the SDK, for making your first request, refer to the [official docs](https://appwrite.io/docs/getting-started-for-flutter#makeRequest).

# Features Appwrite provides

After exploring the docs and learning how to use appwrite, I found that appwrite provides some good features such as,

* User authentication and authorization
    
* Email and SMS services
    
* File storage service to allow developers to store and manage files
    
* Database management to enable developers to store data in documents as well as key-value pair form
    
* Serverless functions, to enable developers to write and deploy serverless functions
    
* Security to help and protect the user data by providing JWT authentication and SSL/TTL encryption.
    

From the above-listed features, I only used some of the basic ones which I earlier used in Firebase like authentication, database and file-management etc...

The authentication service which appwrite provides is too easy to use and it happens so fast as compared to firebase.

I found the file-management and database-management feature quite complex in appwrite as compared to firebase.

So that was all about my reviews of appwrite and its basic features which I used with Flutter.

# Appwrite vs Firebase

Although Appwrite and firebase are both backends as a service (BaaS) platform that provides Developers with a set of tools to build, run and manage their applications.

Here are some key differences between the two:

* **Language Support:** When it comes to appwrite it supports various kinds of programming languages, such as PHP, JavaScript, Swift and Java. On the other hand google's firebase, only support languages which are included in google's tech stack such as Android, Flutter and AngularJS.
    
* **Data Storage:** Appwrite uses a SQL database to store data while Firebase uses NoSQL to store data in document form, This means that two different platforms have different approaches to storing and querying data.
    
* **Real-Time Functionality:** Both Appwrite and Firebase offer real-time functionality, enabling developers to instantly update data across multiple clients. However, google's firebase is built on top of google cloud which may improve scalability and chances of crashing.
    
* **Pricing:** Appwrite offers a free tier, while firebase also has a free tier but appwrite provides some more features such as Email and SMS messaging in their free tier, while google you have to pay for that to use their features.
    

Ultimately, the choice between Appwrite and Firebase will depend on your specific requirements and the technologies you are using to build your application. It's a good idea to evaluate both platforms to see which one best meets your needs.

# Conclusion

Wrapping up this blog and I hope that you've found my review about Appwrite helpful and it made it clear to use which backend for the next application you're going to build. If you have any doubts regarding Flutter or DevOps, Please reach out on [Showwcase](https://showwcase.com/hasnainmakada-99) or [Twitter](https://twitter.com/Hasnain_Makada)

Till Then, Happy Coding 😀