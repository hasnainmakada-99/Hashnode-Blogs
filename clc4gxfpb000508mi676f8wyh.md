# How to authenticate google with Flutter and Firebase

# **Introduction**

Hey everyone I am Hasnain Makada and I am currently working as a Developer Advocate at [Napptive](https://napptive.com/) where I mainly explore the platform in-depth and also advocate Open Source, DevOps, and Flutter to the community. I also write my blogs on [Hashnode](https://hasnainm.hashnode.dev/) and [Showwcase](https://showwcase.com/hasnainmakada-99) where I mainly write about DevOps and Flutter and teach the community.

In this blog, I am going to show you how to authenticate your flutter apps with google with the help of Firebase. We will create a project, configure firebase with flutter, design the app, implement the actual authentication logic, and lastly, we are going to test the app to make sure that the authentication is working properly.

So before moving ahead, let me tell you that this blog is for both (Beginner and intermediate ones) so if you're a beginner who is just getting started with flutter and wants to implement this authentication, you can do that. So let's begin...

# **What is Firebase?**

Firebase is often called a NO-SQL database by developers but it is not limited to databases only. Firebase was originally created by google and it is a complete application development software that enables developers to develop applications in Android, IOS & Web.

Firebase also provides various services such as,

* Analytics: Firebase provides various tools to get the analytics of your apps and detect any false events that occur in your app.
    
* Cloud Firestore: firebase provides a No-SQL database with which you can store the data of your apps inside it and get them easily.
    
* Realtime Database: Firebase provides a cloud-hosted No-SQL real-time database with which you can update data in real-time inside your apps. An example of a real-time database is WhatsApp.
    

That was an overview of what firebase is, but there are many more features that firebase provides to the users which you can check out in its [official documentation](https://firebase.google.com/docs).

# **Setting up the project**

Now that we're ready to create our project, create a new directory in your required drive `mkdir <directory-name>`, and create a new flutter project inside that directory by running this command `flutter create google_signin`. Wait for a few seconds and the project will be created successfully.

After creating the project open it up inside VS Code and the directory structure will look like this.

![img](https://project-assets.showwcase.com/513x475/12496/1669125290881-Google1.png?type=webp align="center")

Add 3 dependencies inside the `pubspec.yaml` file

* `firebase_auth`
    
* `firebase_core`
    
* `google_sign_in`
    

After adding the dependencies successfully, run `flutter pub get` to install the dependencies

Now that we've installed the dependencies successfully, create a new firebase project inside the [firebase console](https://console.firebase.google.com/) and also install the FlutterFire CLI to easily configure your app with Firebase, for more info on how to register visit the [official docs](https://firebase.flutter.dev/docs/cli/)

After configuring your app successfully with Firebase, head over to the authentication tab, and inside the sign methods enable google as a sign-in provider

![img](https://project-assets.showwcase.com/1050x168/12496/1669191597590-Google%25202.png?type=webp align="center")

Now that we've set up our project with firebase we have got one more thing to do and that is to add an SHA certificate inside our project settings without that we will not be able to perform authentication inside our app. In short, firebase will not recognize our app and our app will not perform properly.

If you want to know how to add an SHA certificate to our firebase project, Check out this question on [StackOverflow](https://stackoverflow.com/questions/51845559/generate-sha-1-for-flutter-react-native-android-native-app)

Our project is now set up successfully, so now let's head on toward the design of our app.

# **Designing the app**

The design of the app is going to be very simple, a simple gradient screen, A small box, and a button that will be used for authentication

![](https://project-assets.showwcase.com/12496/1669192432031-Google%25203.png align="center")

Create a new file inside the `/lib` folder and create a file named `googleSignin.dart` inside that paste, the below code, and the design will be created successfully.

```dart
return Scaffold(
      body: Container(
        width: double.infinity,
        height: double.infinity,
        decoration: const BoxDecoration(
          gradient: LinearGradient(
            colors: [
              Colors.blue,
              Colors.red,
            ],
          ),
        ),
        child: Card(
          margin:
              const EdgeInsets.only(top: 200, bottom: 200, left: 30, right: 30),
          elevation: 20,
          child: Column(
            mainAxisAlignment: MainAxisAlignment.spaceEvenly,
            children: [
              const Text(
                "Google Sign In Demo",
                style: TextStyle(
                  fontSize: 25,
                  fontWeight: FontWeight.bold,
                ),
              ),
              Padding(
                padding: const EdgeInsets.only(left: 20, right: 20),
                child: MaterialButton(
                  color: Colors.teal[100],
                  elevation: 10,
                  child: Row(
                    mainAxisAlignment: MainAxisAlignment.start,
                    children: [
                      Container(
                        height: 60.0,
                        width: 60.0,
                        decoration: const BoxDecoration(
                          image: DecorationImage(
                            image: NetworkImage(
                              'https://blog.hubspot.com/hubfs/image8-2.jpg',
                            ),
                            fit: BoxFit.cover,
                          ),
                          shape: BoxShape.circle,
                        ),
                      ),
                      const SizedBox(
                        width: 20,
                      ),
                      const Text("Sign In with Google")
                    ],
                  ),
                  onPressed: () {
                    
                  },
                ),
              )
            ],
          ),
        ),
      ),
    );
```

Inside the sign-in button, the `onPressed` event is there inside which when the user will click, It will perform the authentication logic.

Again create a new file named `HomePage.dart` inside which it will be a home screen. When the user is successfully authenticated it will navigate the user toward the home screen. The home screen will look like this,

![img](https://project-assets.showwcase.com/336x459/12496/1669196201650-Google%25204.png?type=webp align="center")

Now that our design is completed let's move on to authentication.

# **Implementing the actual authentication**

Now inside the `googleSignin.dart` create a FirebaseAuth instance inside the build function of the stateful widget

```dart
final FirebaseAuth auth = FirebaseAuth.instance;
```

Create a new future function named `signUp` which will take a `buildContext` as a parameter and the whole function will be asynchronous. After creating the function, paste this code inside it.

```dart
Future<void> signUp(BuildContext context) async {
    final GoogleSignIn googleSignIn = GoogleSignIn();

    final GoogleSignInAccount? googleSignInAccount =
        await googleSignIn.signIn();

    if (googleSignInAccount != null) {
      final GoogleSignInAuthentication googleSignInAuthentication =
          await googleSignInAccount.authentication;

      final AuthCredential authCredential = GoogleAuthProvider.credential(
        idToken: googleSignInAuthentication.idToken,
        accessToken: googleSignInAuthentication.accessToken,
      );

      UserCredential result = await auth.signInWithCredential(authCredential);

      if (result != null) {
        Navigator.pushReplacement(
            context, MaterialPageRoute(builder: (context) => HomePage()));
      }
    }
  }
```

Firstly we've imported the GoogleSignIn class from the `google_sign_in` package and created an instance of it. The google sign in instance will provide us with several methods to authenticate to google.

After then we created an instance of the googleSignInAccount which will help us to connect with our google account. The `googleSignInAccount` instance will wait for the `googleSign` in instance to successfully sign into the google account.

Then we checked whether the `googleSignInAccount` instance was successful in capturing our google account or not if it will be null, then it will not be redirected to the next screen.

Finally, we've used the AuthCredential class to get the authentication id token and access token for verification purposes of the device in which we are performing the authentication and storing it inside the user credential instance to check whether the email has been authenticated or not. If it has been authenticated successfully, then it will move toward the home screen and we're good to go.

# **Let's test out the app**

![Demo](https://media.giphy.com/media/zosWovq9QWXlwQife3/giphy.gif align="center")

As you can see from the above Video/GIF our authentication is now working perfectly, now if you want to see whether our email has been registered in firebase or not, Go to the firebase console and click on the authentication tab and in the Users section you can see your email

![img](https://project-assets.showwcase.com/1065x/12496/1669306477297-Google%25205.png?type=webp align="left")

#   
**Wrapping Up!!!**

Now its time to wrap up our blog and I hope that by now you have understood how to provide google authentication in flutter using firebase, If you have any further doubts related to it, reach out to me on [Twitter](https://twitter.com/Hasnain_Makada) & [Showwcase](https://showwcase.com/hasnainmakada-99)

Till then, Happy Coding 😀😀😀