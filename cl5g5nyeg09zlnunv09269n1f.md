## Handy Flutter tips for Flutter Developers

### Introduction

Hey everyone in this blog I'm gonna tell you about some of the most useful flutter tips which can come in handy when you are developing applications using Flutter. 

So without wasting any further time let's get started,

### Tip no. 1 - Set preferred orientations

In flutter when we are building our apps some widgets or the layout gets overflowed sometimes when we rotate our virtual emulators. To solve this issue flutter provides the `services.dart` package to us in which we can set our preferred orientations for our app.

This package is so easy to use and we can literally give any type of default orientations to our app also.

**Firstly** import the package `import 'package:flutter/services.dart';`

Now that've imported the package we can use the `SystemChrome` class to set our preferred orientations

```
SystemChrome.setPreferredOrientations([
      DeviceOrientation.portraitUp,
    ]);
``` 
We can use the `setPreferredOrientations` method to give our preferred orientations. You can give this inside any of the build method of your screens

> Note that `setPreferredOrientations` method uses a list of orientations so don't forget to use the list<orientations> inside the method

After applying the orientations you can test it.

### Tip no. 2 - Change the color of the status bar

The `services.dart` package provides us to change the color of our status bar according to our application and this functionality is provided by the `SystemChrome` class.

```
SystemChrome.setSystemUIOverlayStyle(
      SystemUiOverlayStyle(statusBarColor: Colors.blue),
    );
```
We can use the `setSystemUIOverlayStyle` method of the `SystemChrome` class. Inside the method we can use the `SystemUiOverlayStyle` constructor and we can define our custom status bar color to the `statusBarColor` property of it.

There are many more properties of it which you can check out [**here**](https://api.flutter.dev/flutter/services/SystemChrome/setSystemUIOverlayStyle.html)

### Tip no. 3 - Resize to avoid bottom

In flutter sometimes when we build our widgets and layouts they resizes automatically as per the aspect ratio of our device, But there are some layout which we don't want to resize it for that we can use the `resizeToAvoidBottomInset` property of our Scaffold class. This property makes the widgets non - resizable

This is a boolean property so we just have to set it true or false and the jobs done. If you want to know more about this property check out the [official docs](https://api.flutter.dev/flutter/material/Scaffold/resizeToAvoidBottomInset.html)

Here is the example on how to apply the property:
```
 return Scaffold(
      resizeToAvoidBottomInset: false,
      appBar: AppBar(
        title: Text(widget.title),
      ),
)
```

### Tip no. 4 - Remove the debug banner from app

In flutter when we run an application after creating it, it shows a debug ribbon on the app which is used to indicate that our application is still in the debugging phase but when our application is ready for deployment we don't want that right ?

The material App widget provides us the `debugShowCheckedModeBanner` banner property. This is a boolean property and we can set it true or false, By setting it false it removes the debug ribbon from your app

Here is the example on how to apply the property:
```
return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'Flutter Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: const MyHomePage(title: 'Flutter Demo Home Page'),
    );
```
### Conclusion

I hope the tips which I mentioned are going to help you in your upcoming flutter project. Feel free to reach me out on [twitter](https://twitter.com/Hasnain_Makada) and [showwcase](https://showwcase.com/hasnainmakada-99). Keep Fluttering

