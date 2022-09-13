## Circle Avatar widget in flutter and how to use it.

## Introduction

Hey everyone I am Hasnain Makada currently working as a Developer Advocate at [Napptive](https://napptive.com) where I explore the platform deeply and educate the community more and more about DevOps-related topics such as docker, Kubernetes etc... I also like to build android apps using [Flutter](https://flutter.dev/) and in this blog, I'm gonna explain you about a very amazing widget which will come in very handy to you while you're building social media apps using [flutter](https://flutter.dev)

## Circle Avatar widget in Flutter

The circle avatar widget is basically used to display a user's image in a circular shape, the image can be fetched from any source such as from the internet, from the user's device etc... 

The circle avatar widget also provides various properties such as background colour, background image, foreground colour etc... So that we can provide any type of parameters that we want to the widget.

## How to use it?

To create a Circle avatar Widget In flutter we'll first create a new flutter project. So open your terminal and run `flutter create circle`

It will take some time to create the project and once it has been created, paste this code inside the build method.
```
return const Scaffold(
      body: Center(
        child: CircleAvatar(
          radius: 90,
          backgroundImage: NetworkImage(
            'https://www.kidspartyworks.com/images/iron_man_3_graphics_head_iconbug.jpg',
          ),
        ),
      ),
    );

```
Here I've used a network image to get the image from the web, But you can get it from your device and paste it there too. You can also increase the radius property of the image to make the image size bigger and you can also test its various properties of it. For more info [check out](https://api.flutter.dev/flutter/material/CircleAvatar-class.html)

The final output will be like this,

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1663055042787/2jodKfUPE.png align="left")

## Conclusion

I hope that now you have got the idea of what is Circle Avatar widget in flutter and how to use it, If you have any doubts make sure to check out me on [showwcase](https://showwcase.com/hasnainmakada-99) and [Twitter](https://twitter.com/Hasnain_Makada)
