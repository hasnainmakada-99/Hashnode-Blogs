## Alert Dialog widget in Flutter

Hey everyone in this blog I'm gonna talk about the alert dialog widget in flutter and I'll also explain to you how to use it and so on..

Lets get started:

### What is Alert Dialog in Flutter ?

When we are using any application which includes a sign in and sign out facility, when we try to sign out of the application it shows us a dialog or a piece of rectangle in simple terms and it asks us do you really want to log out or not and there are 2 buttons in which one is a cancel button and another is an ok button. If we click on the ok button it tells the application to log out and if we click on the cancel button it keeps us on the same screen.

This is called an Alert Dialog in flutter,  an Alert Dialog is basically a dialog which is used to show warnings to the user or take input from the user based on the controls which you've given to it. The Alert Dialog is a widget in flutter

### Parameters of Alert Dialog

There are mainly 2 parameters are there in alert dialog which we have to use, The first one is the `title` of the alert dialog and the second one is the `actions`.

The title is a constant text which is used to define the title of the dialog, the actions is a list inside which we can provide any component such as text button, text field etc. And they will be displayed when the dialog is called.

Here's a simple example demonstrating the alert dialog widget:

```
  return AlertDialog(
      title: const Text('Alert Dialog'),
      actions: [
        const Text("This is an exmaple of alert dialog")        
        ],
    );

``` 

### Usage of the Alert Dialog widget

You must have seen that when we have to use alert dialog we have to wrap it inside the show dialog widget, The show dialog method is used to show the dialogs on the screen so whenever we want to show any dialog to the user we have to wrap them inside the show dialog widget.

The show dialog widget takes mainly 2 parameters, A context parameter and a builder parameter. The context parameter is used to specify the link to the location of the widget inside the widget tree structure, The builder method is used to define a method inside it in which it takes a context as an argument and you can define your dialog inside the builder method. It will build the dialog on the screen

Here's a simple example showing the use of alert dialog:

```
Future<void> showAlertDialog(BuildContext context){
  return showDialog(
    context: context, 
    builder: (context){
      return AlertDialog(
        title: const Text('Alert Dialog'),
        actions: [
          const Text("This is an exmaple of alert dialog")        
          ],
      );
    }
    );
}

``` 
In the above example we have declared our alert dialog inside a future method in which we have passed the context as a parameter so that it has a link to the location of the widget.

As we have used future functions if we want to see our dialog on our screen we also have to use the `async / await` keywords in our functions to initialize the dialog

You can use this code inside the `onPressed` event of the `TextButton` , Just remember to start the method with the `async` keyword and call this function using the `await` keyword and you're good to go.

### Conclusion

I hope you now understood what is Alert Dialog widget in flutter and how to use it. If you want to refer more about Alert Dialog widget see the official [docs](https://api.flutter.dev/flutter/material/AlertDialog-class.html) and If you have any doubts make sure to check me out on [Twitter](https://twitter.com/Hasnain_makada) and [Showwcase](https://www.showwcase.com/hasnainmakada-99)


