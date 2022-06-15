## AppBar Widget in flutter

Hey everyone in this blog I'm gonna explain you about what is app bar widget in flutter and how can we use it, for what it is and so on...

Lets get started:

### What is AppBar widget ?

As there is a saying in flutter that each and every component that flutter provides they all are widgets and we can customize each and every widget according to our requirement.

So AppBar is also a widget in flutter which is used to define the header or navbar (whatever you can say) in our application and appbar is an optional parameter which we can take when we initialize our scaffold, but it is a prefered way to start coding after initializing the app bar

### Parameters of AppBar

Whenever we initialize an AppBar in flutter mostly take a single parameter which is title and inside the title we define our text using the Text widget

But there also another parameter which is called actions. The actions property is used to define a list of components in a row after the title widget ( [refer](https://api.flutter.dev/flutter/material/AppBar/actions.html) )

In the actions property we can define any custom control we want to use It can be a button, IconButton, popupbutton and so on... We can define any control inside the Appbar which we want to integrate with our application.

The actions property is like list in appbar in which we can insert more than one components too.

### How to add IconButton and PopupButton in Appbar ?

To add an Icon button in appbar we have to use the actions property of the appbar widget, 

Here's a simple example:
```
appBar: AppBar(
          title: const Text('App Bar'),
          actions: [
              IconButton(
                onPressed: null,
                icon: const Icon(Icons.recent_actors),
              )
          ]
),

``` 
Output:
- Icon Button on the right side
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1655272895181/Rm0VICt-O.png align="left")

As we can see from the above code example we can define a Icon button inside appbar easily but there is a problem over here.

We can only select one icon button at a time, means if we want to define so many operations that we want to perform inside the appbar then every time we cannot define a new button right ? it will eventually increase the complexity at a larger scale

To solve this problem we can use the Popupbutton widget to define a list of operations inside the appbar, The popupbutton is a parent widget which is used to define popupmenuitems inside it so it will show use only 3 buttons on the appbar and when we click on the 3 buttons it will show us the list of the pop up menu items.

Here's a simple way to implement this functionality
``` 
enum menuItem {
  logout, signIn
}

 appBar: AppBar(
          title: const Text('App Bar'),
          actions: [
             PopupMenuButton<menuItem>(
                itemBuilder: (context){
                  return const [
                    
                  PopupMenuItem<menuItem>(
                    value: menuItem.logout,
                    child: const Text('Logout'),
                  ),
                  
                   PopupMenuItem<menuItem>(
                    value: menuItem.signIn,
                    child: const Text('Sign In'),
                  ),
                  
                  ];
                    
                },
             )
          ]
),

``` 
Output:

- Dots on the right side of the appbar
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1655272764841/WzLIgDPRi.png align="left")
- After clicking on the dots
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1655272827186/yEDNqN2Cu.png align="left")

As we can see from the above example in we can add popup menu item inside the pop up menu button widget, the popup button widget is a generic so it can hold the values of several data types, Here we have provided the Enum menu Item as a generic data type to both the button as well as the menu item

The item builder property of pop up button widget is called when the button is pressed to create the items to show in the menu. ( [refer](https://api.flutter.dev/flutter/material/PopupMenuButton/itemBuilder.html) )

If we want to return menuItems inside the menu button we have to compulsorily include them inside the const [] list, because the items which are included are going to be constant all over the app, they are not going to change and if we dont provide constant to it, it will throw error to use to make it constant

### Conclusion

I hope you now understood what is appBar widget in flutter and how to use and add icon buttons and popupmenuitems inside it. If you want to refer more about appBar see the official [docs](https://api.flutter.dev/flutter/material/AppBar-class.html) and If you have any doubts make sure to check me out on [Twitter](https://twitter.com/Hasnain_Makada) and [Showwcase](https://showwcase.com/hasnainmakada-99)

